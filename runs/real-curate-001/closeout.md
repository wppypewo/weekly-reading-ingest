# Weekly Reading Ingest v0 — Closeout（real-curate-001）

## 1. 本次目標

跑通 Weekly Reading Ingest v0 第一個完整閉環：`curate → 候選報告 → 人工確認 → ingest preview → 正式 ingest → kb:index → kb:lint → commit`，用真實搜尋結果驗證兩份 SKILL.md（`weekly-reading-curate` / `weekly-reading-ingest`）的規格是否可執行、是否有遺漏。

## 2. 最終入庫文章

- Title: A Survey of Development Workflows in the Coding Agent Era
- Author: 逆瀬川ちゃん（Sakasegawa-chan, @gyakuse）
- URL: https://nyosegawa.com/en/posts/coding-agent-workflow-2026/
- Domain: `ai-workflow`
- Source folder: `articles`

## 3. 為什麼選 Main Pick

不只看總分（與 Backup B 並列 21）。Main Pick 勝出依據：

- 直接對應本週實際任務（設計 `weekly-reading-curate` / `weekly-reading-ingest` 兩個 skill 文件）
- 提供至少 5 個結構化決策框架，Idea Density 全場最高（5/5）
- Relevance 全場最高（5/5）——可立即拿來自我檢查現有 SKILL.md
- domain 落入既有 `ai-workflow` 無疑義，不需經過 `DOMAIN_DECISION`

## 4. 兩篇備選與未選原因

- **Backup A**：《Evergreen notes》— Andy Matuschak — https://notes.andymatuschak.org/Evergreen_notes
  - Scores: SQ 5 / ID 4 / LV 5 / RV 3 / OF 2（總分 19）
  - 未選原因：Source Quality、Long-term Value 皆最高，但 Relevance 與本週主軸（Claude Code agentic workflow）關聯較弱，且**無法歸入既有五個 concept domain**——刻意保留作為 domain 邊界測試案例，驗證若被選中會正確觸發 `DOMAIN_DECISION`（本次未發生，因使用者選的是 Main Pick）。
- **Backup B**：《Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers》— Pengfei Du — https://arxiv.org/html/2603.07670v1
  - Scores: SQ 5 / ID 4 / LV 5 / RV 4 / OF 3（總分 21，與 Main Pick 並列）
  - 未選原因：總分打平 Main Pick，但屬學術綜述,篇幅長、偏理論形式化,Relevance 與 Obsidian Fit 略低——用來驗證「不能只看總分」這條規則在真實候選上是否站得住,結果證明站得住。

## 5. 實際寫入 vault 的檔案清單

```
raw/sources/articles/2026-W26-coding-agent-workflow-survey.md
wiki/concepts/ai-workflow/agents-md-design-checklist.md
wiki/outputs/weekly-reading/project-links/2026-W26-coding-agent-workflow-survey.md
wiki/outputs/weekly-reading/review-cards/2026-W26-coding-agent-workflow-survey.md
meta/weekly-reading/log.md
meta/index.md（script 自動更新）
meta/lint.md（script 自動更新）
```

## 6. 實際 commit hash

```
e0161bb 新增每週精讀策展首篇入庫
```

## 7. Lint 結果

```
Checked 56 files — Blocking: 0  Warnings: 12
[Blocking] Missing type: 0 / Broken links: 0
[Review Warnings] Imported (needs src): 12 / Active w/o source: 0 / Empty domain: 0 / Processed w/o concept: 0
```

Blocking=0、Broken links=0，新增的 weekly-reading 檔案未造成任何 lint error。12 個 Warnings 全部是既有 legacy「Imported (needs src)」項目，與本輪無關。

## 8. needs_review=1 的原因

完全由本輪新 source note 造成：`raw/sources/articles/2026-W26-coding-agent-workflow-survey.md` 的 `processed: false`。這是預期狀態——weekly-reading ingest 流程本身不負責把 source 標記為 `processed: true`，那是既有 `kb-ingest` skill 的職責,兩者刻意保持分工,不混用。

## 9. 本次做對的流程設計

- **兩階段分離徹底執行**：curate 全程未寫 vault，ingest 只在收到「確認主選」後才動作，中間的等待確認狀態確實發揮了審查閘門的作用。
- **preview-first 流程有效**：在正式寫入前先產出 6 份 preview 檔並逐項自我審核，提前抓出 3 處問題（excerpt 誤標、project-link 漏檢查點、weekly-log 漏備選評分），避免直接污染 vault 後才發現。
- **safety checklist 確實被當作硬性閘門使用**，不是裝飾性文件——每次寫入前都逐項列出並核對，而不是憑印象判斷。
- **domain 邊界刻意保留測試案例（Backup A）**，證明 `DOMAIN_DECISION` 機制在真實內容上是可執行的判斷,不是紙上設計。
- **檢查現有自動生成檔案的寫入機制**（`kb:index` 寫 `meta/index.md`、`kb:lint` 寫 `meta/lint.md`），確認只透過 script 更新、未手動編輯,且逐筆核對沒有刪除既有條目。

## 10. 本次發現並修正的問題

- **Free Access 二次檢查**：原規格只在 curate 階段把關付費牆，dry-run 測試發現 ingest 階段沒有第二道防線,後補上 `FREE_ACCESS_CHECK` 節點與 Safety Checklist 對應項目。
- **Domain decision**：原規格的「無法歸入既有 domain」處理過於寬鬆（允許部分寫入）,後修正為硬性閘門——domain 未決時不可寫任何一類筆記,必須先取得三選一二次確認。
- **Source excerpts 不可偽裝成引文**：source-note-preview 審核時發現一段中文摘要被誤標成「節錄」（用引言格式呈現),修正為只保留真正的原文引述,摘要另外獨立成段並標明「重寫非翻譯」。
- **Concept note 不一次拆太多**：原候選報告建議從一篇文章拆 3 個 concept note,審核後收斂為只 ingest 1 篇,其餘 2 個留在 source note 的「後續可萃取概念」區塊,避免過度萃取稀釋知識庫。
- **Project-link 不假造 wiki/projects**：因為 `wiki/projects/` 目前沒有 `weekly-reading-ingest` 專案資料夾,project-link note 改為純文字描述關聯,不建立任何指向不存在路徑的 wikilink。
- **Weekly log 要包含備選評分與 status**：審核時發現兩處遺漏——備選原本只記標題/連結/理由,缺評分;log 條目原本完全沒有 status 欄位,無法區分 preview 與正式狀態。兩者都已補上。

## 11. 下一週使用時應沿用的規則

- 候選報告先產出，不直接 ingest，等待「確認主選 / 改選備選 A / 改選備選 B」三種語句之一。
- ingest 前一律先產 preview（6 份檔案：source / concept / project-link / review-card / weekly-log / safety-check），自我審核通過後才正式寫入。
- 正式寫入後固定跑 `npm run kb:index`，需要時才跑 `npm run kb:lint`（因為會覆寫 `meta/lint.md`，先回報再決定）。
- concept note 一次只 ingest 1 篇，其餘候選概念留在 source note 備查。
- 備選只存標題、連結、推薦理由、評分，不完整 ingest。
- domain 與 Free Access 兩項都是硬性閘門，未決時不寫任何檔案，不可部分寫入。
- 法文來源依內容型態進 `articles` 或 `papers`，不進 `raw/sources/french/`。
- commit 範圍只包含 vault 內實際變更的檔案，工具專案 `weekly-reading-ingest` 不納入 vault commit。

## 12. 不應擴大的範圍

- 不自動化排程（不建 cron / launchd / Task Scheduler）。
- 不做多使用者、不做 App/Web、不接 Notion/Google Drive。
- 不因為這次跑通就放寬 domain 或 Free Access 的硬性檢查。
- 不因為流程順暢就一次處理多篇文章——v0 的設計前提是「一次只處理一筆」，這個限制要繼續沿用,不要因為效率考量就批量化。
- 不在沒有真正需要時，主動修改 `tools/kb/*.mjs` 或既有 kb-* skills。
