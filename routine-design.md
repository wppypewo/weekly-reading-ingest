# Weekly Reading Ingest — Claude Routine 使用設計

> 本檔只設計「Claude routine 每週六 10:07 如何使用 `weekly-reading-curate`」。**不建立 OS 排程器**（不做 cron / launchd / Windows Task Scheduler），排程行為由 Claude routine 本身負責（對應 `weekly-reading.config.json` 的 `routine.provider: "claude"`）。

> **routine 實測狀態（accurate）：尚未真實測試。** 至今全為手動執行，`config.routine.tested = false`。manual loop 已完成並通過一次真實 ingest，但「每週六 10:07 自動觸發 curate」這個 routine 行為從未實跑。**暫不建議立刻掛 routine**，建議先手動跑 2–3 週再開。本檔不得把 routine 寫成已完成。

> **執行位置：雲端 routine**（使用者 2026-10-12 決定）。雲端適配（vault 路徑解析、報告推 `claude/` 分支、網路與 setup script）已寫進本檔 4.6，**同樣未實測**；第一次手動試跑的檢查清單在 [`runs/routine-test-001/checklist.md`](runs/routine-test-001/checklist.md)。

> 失敗情境見 [`FAILURE-HANDLING.md`](FAILURE-HANDLING.md)；strict / quick 模式見 [`MODES.md`](MODES.md)；安全規則見 [`SAFETY.md`](SAFETY.md)。

## 4.1 Routine 定位

- Claude routine 每週六 10:07（Asia/Taipei）觸發 `weekly-reading-curate`，這是 routine 的行為，不是本機排程器的行為（`localScheduler.enabled` 固定 `false`）。
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
   決定 vault 根目錄：環境變數 CLAUDE_CODE_REMOTE=true 時（雲端），用 toolRoot 加上
   config.cloud.vaultRootRelative；不存在就找 toolRoot 同層 git remote 對應 config.cloud.vaultRepo 的目錄；
   仍找不到就停止並回報同層有哪些目錄，不產報告。不是雲端時用 config.vaultRoot。
   雲端時 vault clone 只讀，不得在其中建立、修改、commit 任何檔案。
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
6. 預判每篇候選的 concept domain，只能是 `weekly-reading.config.json` 當下
   `allowedConceptDomains` 裡的值；本檔不重抄清單，避免與設定漂移。
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
10. 報告輸出到 Claude 界面，另存一份到工具專案的 config.paths.runsDir 下 YYYY-Www/candidates.md
    （同週已存在則改 candidates-v2.md，不覆寫）。雲端時在工具 repo 開 claude/weekly-reading-YYYY-Www 分支，
    只 commit 這份報告並推到該分支；不得推 master、不得開 PR、不得 commit 其他檔案。
    推送失敗時報告只留在對話中，不視為失敗，也不嘗試寫入 Obsidian vault 來代替保存。
    報告「本週主題判斷」要寫出讀到的 vault HEAD commit 與日期；被網路擋下的網域列在報告末尾。
11. 報告產出後停在「等待確認」狀態。
    嚴禁：不得寫入 Obsidian vault 任何路徑；不得建立 source / concept / project-link / review-card；
    不得因總分最高自動決定主選；不得推薦付費牆內容作為主選；不得呼叫 weekly-reading-ingest。
```

## 4.3 每週人工操作流程

1. 手機提醒響起（純提醒,不連任何系統)。
2. 打開 Claude，到 claude.ai/code/routines 點本週那次 run（每次 run 是一個獨立 session）。run 列表的綠燈只代表沒有基礎設施錯誤，要打開 transcript 才知道 curate 有沒有成功。
3. 查看 `weekly-reading-curate` 產出的候選報告（1 主選 + 2 備選,或降級報告)。
   - **自己帶文章來的週**：routine 照跑，不另加偵測機制。在該次 run 的 session 回「補連結後重評」並貼連結（SKILL 本來就支援手動連結與自動候選混合評分），或回「本週跳過」後另開本機 session 處理你的文章。
4. 選擇以下六種互動選項之一：
   - 確認主選
   - 改選備選 A
   - 改選備選 B
   - 補連結後重評
   - 重新搜尋
   - 本週跳過
5. **只有「確認主選」「改選備選 A」「改選備選 B」三者會進入 ingest 流程**;其餘三項（補連結後重評、重新搜尋、本週跳過）都不會觸碰 vault。
   選了前三項之一時，ingest 一律在本機做：先 `git fetch` 取得 routine 推的 `claude/weekly-reading-YYYY-Www` 分支，把該週 `candidates.md` 帶回本機（checkout 該檔或 merge 該分支，由使用者決定），再在本機 session 說出確認語句。
6. 即使選了前三項之一,**ingest 前仍要先產 preview**：strict mode 產 5 份（source-note / concept-note / project-link / weekly-log / safety-check；review-card 2026-08-01 起停產）,quick mode 合併為 1 份 summary preview;存在 `config.paths.runsDir`/<week>/`config.paths.previewDirName`/（見 [`MODES.md`](MODES.md)）。
7. Preview 內容需經審核通過（檢查 excerpts 是否過長、domain 是否合理、評分是否有區分度、project-link 是否假造路徑等）才能進入正式寫入。
8. Preview 通過後才正式寫入 vault 對應路徑（`raw/sources/`、`wiki/concepts/`、`meta/weekly-reading/log.md`）。
9. 寫入後依序執行 `npm run kb:index`；接著告知 `npm run kb:lint` 會覆寫 `meta/lint.md`，取得確認後執行 lint。lint 通過後（Blocking=0、Broken links=0、新增檔案無錯誤）才 commit。
10. Commit 範圍只含 vault 內本次實際變更的檔案,不含工具專案（`toolRoot`,即含本 config 的目錄,有自己的 git repo)。預設不 push,除非另行要求。

## 4.4 下週不應自動化的部分

- 不自動 ingest——永遠需要人工明確說出「確認主選 / 改選備選 A / 改選備選 B」。
- 不自動寫 vault——curate 階段、preview 階段都不寫,只有經過確認與 preview 審核後才寫。
- 不自動 commit。
- 不自動 push。
- 不自動新增 domain——只能用 `allowedConceptDomains` 當下列出的值；無法歸入時走 `DOMAIN_DECISION`，不得自創新 domain 或塞進 `other`。
- 不自動建立 `wiki/projects/` 下的新專案資料夾——project-link note 一律放對應的 `wiki/concepts/<domain>/`,即使該專案目前在 vault 沒有對應資料夾,也不得自動建立。
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
| 雲端找不到 vault clone、網路擋下來源、缺 `pdftotext`、推 `claude/` 分支失敗 | 見 [`FAILURE-HANDLING.md`](FAILURE-HANDLING.md) C 區；confirmed ingest 一律在能存取 `config.vaultRoot` 的本機執行 |

## 4.6 雲端環境設定（2026-10-12，未實測）

依據：官方文件 [Routines](https://code.claude.com/docs/en/routines)、[Cloud environments](https://code.claude.com/docs/en/cloud-environments)、[Settings in cloud sessions](https://code.claude.com/docs/en/settings#settings-in-cloud-sessions)，2026-10-12 讀取。Routines 目前是 research preview，行為可能變。

### Repositories

- 掛兩個：`zhuang060329-bit/weekly-reading-ingest`、`zhuang060329-bit/ricky-knowledgebase`。每次 run 都從 GitHub 預設分支重新 clone。
- 多 repo 的 session 從「所有 clone 的上一層」開始，各 repo 的 `.claude/settings.json` 只讀 `enabledPlugins` 等兩個鍵。官方文件沒寫 clone 目錄名，`config.cloud.vaultRootRelative` 的 `../ricky-knowledgebase` 是推測值，試跑時確認。
- 因為 session 不在工具 repo 內啟動，專案 skill 不一定自動載入。routine prompt 要明寫：「先讀 `weekly-reading-ingest/.claude/skills/weekly-reading-curate/SKILL.md`，照它執行」。
- vault 只能讀到**已推送**的內容。2026-10-12 實測 `git ls-remote`：vault 遠端 HEAD `efd4ff3` 與本機相同。之後若本機改了 `schema/context/current-focus.md` 沒推，routine 會讀到舊版。

### 分支保護（不設 ruleset 的原因）

官方文件寫明：在 Anthropic 託管環境，GitHub ruleset 套用在你連接的 GitHub 身分上，該身分能 bypass 的規則擋不住 routine。routine 推送用的就是你的身分，所以：

- 設一條連你自己也擋的 master ruleset，會同時擋掉你本機推 master；
- 設成 owner 可 bypass，routine 也能 bypass。

結論：ruleset 分不出「你」和「routine」，不設。限制靠 prompt 與 SKILL 的明文禁止（只推 `claude/` 分支、vault 只讀），每次 run 由你看 transcript 與 diff 核對。這是殘留風險：vault repo 掛在 routine 上時，技術上它有推送權限。

### Network access

- Default 環境是 **Trusted**，只放行套件庫、GitHub、雲端 SDK 網域，學術站會回 `403 host_not_allowed`。
- 建議用 **Custom**，勾「Also include default list of common package managers」（`apt install` 需要 `*.ubuntu.com`）。起始清單（每行一個）：

```text
arxiv.org
*.arxiv.org
*.nber.org
*.ssrn.com
doi.org
*.doi.org
api.crossref.org
api.openalex.org
*.semanticscholar.org
academic.oup.com
*.econometricsociety.org
*.uchicago.edu
aeon.co
psyche.co
*.noemamag.com
nautil.us
theconversation.com
```

- 作者個人頁、大學 repository 每週不同，清單一定會漏。漏掉的照 FAILURE-HANDLING C 區處理，報告末尾列出被擋網域，你再決定要不要加。`*.edu` 這種只到頂級網域的萬用字元是否有效，文件沒寫，未驗證。
- 改用 **Full** 可以免維護清單，代價是 routine 沒有權限確認，讀到的網頁內容若含惡意指示，可外送的目的地不受限。
- 未確認：WebSearch／WebFetch 工具的請求是否走這份 allowlist。官方文件只說 GitHub、MCP connector、network secrets 的 host、Anthropic API 不經過 allowlist，沒有提這兩個工具。試跑時看 transcript 有沒有 403。

### Setup script

雲端 VM 是 Ubuntu 24.04，預裝 Python 3、Node 22、git、gh、jq，文件列表沒有 `poppler-utils`。setup script 以 root 執行：

```bash
#!/bin/bash
# 安裝 pdftotext（poppler-utils），供讀取論文 PDF
apt update && apt install -y poppler-utils
```

### 其他設定

- Connectors：建立時預設全部勾選，curate 不需要任何 connector，全部移除。
- 排程：每週六 10:07（Asia/Taipei），避開整點延遲。試跑通過前不加排程 trigger，只用 Run now。
- Model：建立表單可選，沒有特別要求就用預設。
