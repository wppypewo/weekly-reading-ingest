# Weekly Reading Ingest — Claude Routine 使用設計

> 本檔只設計「Claude routine 每週六 10:00 如何使用 `weekly-reading-curate`」。**不建立 OS 排程器**（不做 cron / launchd / Windows Task Scheduler），排程行為由 Claude routine 本身負責（對應 `weekly-reading.config.json` 的 `routine.provider: "claude"`）。

> **routine 實測狀態（accurate）：尚未真實測試。** 至今全為手動執行，`config.routine.tested = false`。manual loop 已完成並通過一次真實 ingest，但「每週六 10:00 自動觸發 curate」這個 routine 行為從未實跑。**暫不建議立刻掛 routine**，建議先手動跑 2–3 週再開。本檔不得把 routine 寫成已完成。

> 失敗情境見 [`FAILURE-HANDLING.md`](FAILURE-HANDLING.md)；strict / quick 模式見 [`MODES.md`](MODES.md)；安全規則見 [`SAFETY.md`](SAFETY.md)。

## 4.1 Routine 定位

- Claude routine 每週六 10:00（Asia/Taipei）觸發 `weekly-reading-curate`，這是 routine 的行為，不是本機排程器的行為（`localScheduler.enabled` 固定 `false`）。
- 手機備忘錄 / 提醒事項只提醒使用者去 Claude 確認本週主選（`phoneReminder.externalOnly: true`），不連 Obsidian、不觸發任何寫入，不是系統依賴。
- Claude routine 執行 curate 時**不直接寫 Obsidian vault**——curate 階段的唯一輸出是候選報告。
- 未確認主選前（即未收到「確認主選」「改選備選 A」「改選備選 B」三者之一），**不得進入 ingest**，不論是 routine 本身或後續任何對話都不可越過這個閘門。

## 4.2 Routine Prompt 草案

```text
你現在要執行 weekly-reading-curate。

1. 在工具專案根目錄（含本 config 的目錄）讀取 weekly-reading.config.json，
   取得 vaultRoot、allowedConceptDomains、allowedSourceFolders、weeklyPickCount、
   freeOnly、mainPickThreshold、paths、modes。
   後續所有路徑一律以 config 為準，不要把任何絕對路徑寫死在 prompt 主體中。
   若無法存取本機檔案（找不到 config），只在 Claude 界面輸出候選報告，不寫任何檔。
2. 讀取以下 vault context（相對於 config.vaultRoot，只讀，不寫）：
   - schema/context/current-focus
   - wiki/projects/*/current-status
   據此判斷本週候選方向；若使用者本次另外指定主題或排除主題，以使用者指定為準。
3. 搜尋本週候選，只收免費可讀內容（freeOnly: true）。
   優先：原始論文、作者原文、公司研究、深度 essay、專業媒體。
   排除：SEO 文章、短新聞、內容農場、純轉述、付費牆內容作為主選、只因熱門而推薦。
4. 對每篇候選評五項分數（Source Quality / Idea Density / Long-term Value / Relevance / Obsidian Fit，
   1–5，每項附一句理由，評分要有區分度；若三篇都屬高分候選，必須清楚說明各自弱點與排序理由，不能只給接近滿分而沒有取捨）。
5. 每篇明確標記 Free Access: Yes / No / Unclear。
   - No 不得列為主選。
   - Unclear 原則上不得列為主選，除非有明確免費替代版（arXiv、作者 PDF、官方開放版）並寫出來源。
6. 預判每篇候選的 concept domain，只能是 allowedConceptDomains 裡的值
   （ai-engineering / ai-workflow / design / finance / french）。
   - 無法歸入者：Obsidian Fit 降低，原則上不得列為主選，可標記「需要人工 domain 決策」。
   - 不得使用 other，不得新增 domain。
7. 判斷主選：不能只看總分，需說明為何是主選、為何勝過兩篇備選、補的知識缺口、
   適合沉澱的概念、可能的專案連結、限制與風險。
   Main Pick 軟門檻（config.mainPickThreshold）：原則上須 Source Quality ≥ 3、Relevance ≥ 3、
   Free Access = Yes、domain ∈ allowedConceptDomains；未滿足者不得自動為 Main Pick，標「需要人工決策」。
8. 候選不足時不要硬湊——可以少於 1 主選 + 2 備選，或回報「本週無合格候選」。
9. 產出候選報告（格式：本週主題判斷 / Main Pick / Backup A / Backup B / 五項評分表 /
   主選勝出理由 / 風險與限制 / 建議 concept note / 可能 project link / Free Access 判斷依據 /
   互動選項固定六項：確認主選、改選備選 A、改選備選 B、補連結後重評、重新搜尋、本週跳過）。
10. 報告輸出到 Claude 界面。若本地 Claude Code 可存取檔案，另存一份到
    工具專案的 config.paths.runsDir 下 YYYY-Www/candidates.md（同週已存在則改 candidates-v2.md，不覆寫）；
    若無法存取本機檔案，只輸出在對話中，不視為失敗，也不嘗試寫入 Obsidian vault 來代替保存。
11. 報告產出後停在「等待確認」狀態。
    嚴禁：不得寫入 Obsidian vault 任何路徑；不得建立 source / concept / project-link / review-card；
    不得因總分最高自動決定主選；不得推薦付費牆內容作為主選；不得呼叫 weekly-reading-ingest。
```

## 4.3 每週人工操作流程

1. 手機提醒響起（純提醒,不連任何系統)。
2. 打開 Claude。
3. 查看 `weekly-reading-curate` 產出的候選報告（1 主選 + 2 備選,或降級報告)。
4. 選擇以下六種互動選項之一：
   - 確認主選
   - 改選備選 A
   - 改選備選 B
   - 補連結後重評
   - 重新搜尋
   - 本週跳過
5. **只有「確認主選」「改選備選 A」「改選備選 B」三者會進入 ingest 流程**;其餘三項（補連結後重評、重新搜尋、本週跳過）都不會觸碰 vault。
6. 即使選了前三項之一,**ingest 前仍要先產 preview**：strict mode 產 6 份（source-note / concept-note / project-link / review-card / weekly-log / safety-check）,quick mode 合併為 1 份 summary preview;存在 `config.paths.runsDir`/<week>/`config.paths.previewDirName`/（見 [`MODES.md`](MODES.md)）。
7. Preview 內容需經審核通過（檢查 excerpts 是否過長、domain 是否合理、評分是否有區分度、project-link 是否假造路徑等）才能進入正式寫入。
8. Preview 通過後才正式寫入 vault 對應路徑（`raw/sources/`、`wiki/concepts/`、`wiki/outputs/weekly-reading/`、`meta/weekly-reading/log.md`）。
9. 寫入後依序執行 `npm run kb:index`；接著告知 `npm run kb:lint` 會覆寫 `meta/lint.md`，取得確認後執行 lint。lint 通過後（Blocking=0、Broken links=0、新增檔案無錯誤）才 commit。
10. Commit 範圍只含 vault 內本次實際變更的檔案,不含工具專案（`toolRoot`,即含本 config 的目錄,有自己的 git repo)。預設不 push,除非另行要求。

## 4.4 下週不應自動化的部分

- 不自動 ingest——永遠需要人工明確說出「確認主選 / 改選備選 A / 改選備選 B」。
- 不自動寫 vault——curate 階段、preview 階段都不寫,只有經過確認與 preview 審核後才寫。
- 不自動 commit。
- 不自動 push。
- 不自動新增 domain——只能用 `allowedConceptDomains` 既有五個值,無法歸入時走 `DOMAIN_DECISION`,不得自創新 domain 或塞進 `other`。
- 不自動建立 `wiki/projects/` 下的新專案資料夾——project-link note 一律放 `wiki/outputs/weekly-reading/project-links/`,即使該專案目前在 vault 沒有對應資料夾,也不得自動建立。
- 不自動把 Backup 完整入庫——備選永遠只記標題、連結、推薦理由、評分到 weekly log,不建立各自的 source/concept/project-link/review-card。
- 不自動把文章全文複製進 vault——source note 只保留短節錄（引用線索用）與繁體中文重寫摘要,不貼整篇原文。

## 4.5 失敗處理

| 情境 | 處理 |
|---|---|
| 找不到足夠好候選 | 不硬湊，回報「本週無合格候選」，停在 IDLE，不產報告、不寫 vault |
| 只有 1 篇達標 | 產降級報告：Main Pick 正常評分，Backup 欄位寫「無達標備選」，不補低品質文章 |
| Free Access 不明 | 不得當主選；無免費替代版則降為備選或剔除；若仍被誤選進 ingest，`FREE_ACCESS_CHECK` 直接 ABORT,不寫任何一類筆記 |
| domain 不屬於 `allowedConceptDomains` | 進入 `DOMAIN_DECISION`，停止寫入，等待三選一二次確認（指定既有 domain / 批准不產 concept note / 取消 ingest），未決前不可部分寫入 |
| 我沒有確認 | 停在 `AWAITING_CONFIRMATION`，模糊語句（看看/可以嗎/先放著/之後再說）不算確認，不寫 vault |
| 我跳過 | 進 `SKIPPED` → `IDLE`，不寫 vault |
| routine 無法存取本機 D 槽 | 候選報告只在 Claude 界面輸出，不產生 `runs/` 暫存檔，也不嘗試寫入 Obsidian vault 來代替保存；confirmed ingest 仍須在能存取 vault 的本機環境執行 |
