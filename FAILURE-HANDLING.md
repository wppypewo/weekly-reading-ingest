# Weekly Reading Ingest — FAILURE HANDLING

> 從 skill 文件抽出的失敗情境處理，集中於此維護。**執行 curate 或 ingest 前必讀。**
> 共通原則：任何失敗都不得用「記憶印象」或「快取」硬湊內容；不得為了完成流程而放寬安全閘門；不確定就停下回報，不要默默繼續。

## A. curate 階段失敗情境

| 情境 | 處理 |
|---|---|
| 找不到足夠好候選 | 不硬湊，回報「本週無合格候選」，停在 IDLE，不產報告、不寫 vault |
| 只有 1 篇達標 | 產降級報告：Main Pick 正常評分，Backup 欄位寫「無達標備選」，不補低品質文章 |
| Free Access 不明 | 不得當主選；無免費替代版則降為備選或剔除；標 `Free Access: Unclear` |
| **WebFetch 抓不到全文** | 不可用記憶硬湊；只讀到 abstract / metadata 不能當作已完整閱讀；Idea Density 與 Obsidian Fit 必須降低；內容不足者原則上不得列為 Main Pick |
| **arXiv / blog 暫時連不上** | 可重試一次；可找官方替代入口（arXiv 鏡像、作者站、官方開放版）；仍不可用快取印象硬寫；無法驗證 Free Access 時標 `Unclear` |
| **candidates.md 已存在（同週重跑）** | 不得默默覆寫；改存 `candidates-v2.md`（同週遞增），或停止並回報讓使用者決定 |

## B. ingest 階段失敗情境

| 情境 | 處理 |
|---|---|
| 我沒有確認 | 停在 `AWAITING_CONFIRMATION`；模糊語句（看看/可以嗎/先放著/之後再說）不算確認，不寫 vault |
| 我改選備選 | 走對應 INGEST_A / INGEST_B；若該備選低分，先顯示警示再續（不需第三次確認，除非同時觸發 domain / Free Access 問題） |
| 我跳過本週 | 進 `SKIPPED` → `IDLE`，不寫 vault |
| Free Access = No / Unclear | `FREE_ACCESS_CHECK` 直接 ABORT，不寫任何一類筆記，無三選一補救 |
| domain 不屬於 `allowedConceptDomains` | 進入 `DOMAIN_DECISION`，停止寫入，等待三選一二次確認；未決前不可部分寫入 |
| **vault 檔名衝突** | 不覆寫；停止並回報衝突路徑，等待使用者決定改名或取消 |
| **`npm run kb:index` 失敗** | 停止；回報已寫入哪些筆記、index 未更新；不 commit；不手動亂改 `meta/index.md` |
| **`npm run kb:lint` 發現 Blocking** | 不 commit；只修本輪新增/修改的檔案；不擴大修 legacy；修完重跑 lint |
| **commit 前工作區有其他未提交變更** | 停止；回報所有變更清單；本週 commit 只能用 `git add <逐一指定的本輪檔案>`，不得 `git add -A` / `git add .`，不把不相關變更包進 commit |

## C. 執行環境失敗情境

| 情境 | 處理 |
|---|---|
| routine 無法存取本機檔案（例如 Mac 遷移前後路徑變動、或無檔案系統權限） | 候選報告只在 Claude 界面輸出，不產生 `runs/` 暫存檔，也不嘗試寫入 Obsidian vault 代替保存；confirmed ingest 仍須在能存取 `config.vaultRoot` 的本機環境執行 |
| `config.vaultRoot` 指向的路徑不存在（例如剛換機器尚未改 config） | 停止；回報 vaultRoot 不可達；要求使用者先更新 `weekly-reading.config.json` 的 `vaultRoot`，不要猜測新路徑 |

## D. 內容品質失敗情境

| 情境 | 處理 |
|---|---|
| 只讀到摘要卻被要求 ingest | 在 source note 的 caveats 明確標「未取得全文，僅依摘要/metadata」，confidence 標 `low` 或 `medium`，不偽稱已完整閱讀 |
| project-link 找不到真實專案關聯 | 寫「本週沒有明確專案連結」，不硬連既有專案 |
| review card 沒有有價值的問題 | 出 0 題或 1 題，於檔內說明原因，不硬湊到 3 題、不出「請簡述本文」類低價值題 |
