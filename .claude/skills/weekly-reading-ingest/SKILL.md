---
name: weekly-reading-ingest
description: 每週精讀策展——使用者確認主選後，把確認對象寫入 Obsidian vault（source / concept / project-link / review-card / weekly log）。只在收到「確認主選」「改選備選 A」「改選備選 B」時觸發。
---

# weekly-reading-ingest

每週精讀策展的「確認後寫入」階段。

## 實作狀態（accurate）

- v0 **已完成一次**人工確認後的正式 ingest（首篇：commit `e0161bb`）。
- 已驗證閉環：候選報告 → 人工確認 → preview → 正式寫入 → `kb:index` → `kb:lint` → commit。
- **Claude routine 自動觸發尚未真實測試**（至今全為手動執行）；掛 routine 前建議先手動跑 2–3 週。
- 本 skill 已可實際寫檔，但**每次都必須遵守確認、preview、safety checklist，不得跳過**。

## 執行前必讀

- [`SAFETY.md`](../../../SAFETY.md)：寫入範圍、紅線、Safety Checklist。
- [`FAILURE-HANDLING.md`](../../../FAILURE-HANDLING.md)：失敗情境處理。
- [`MODES.md`](../../../MODES.md)：strict / quick 模式差異（安全閘門兩模式相同）。
- 路徑與白名單一律以 `weekly-reading.config.json` 為準，不在本檔散落絕對路徑。

## 觸發條件

只接受以下三種語句之一：**確認主選 / 改選備選 A / 改選備選 B**。
其他語句（看看 / 可以嗎 / 先放著 / 之後再說 / 無回應）**不得觸發**，維持等待確認狀態。

## 前置條件

必須存在候選報告（`config.paths.runsDir`/YYYY-Www/candidates.md 或當前對話中的報告），且含評分與主選勝出理由，否則先要求補齊。

## 核心規則摘要（細節見 SAFETY.md）

- **Free Access 二次攔截**：curate 已把關，但 ingest 必須獨立再檢；Free Access = No / Unclear → ABORT，不寫任何一類筆記，無三選一補救。
- **Main Pick 軟門檻**：Source Quality ≥ 3、Relevance ≥ 3、Free Access = Yes、domain ∈ allowedConceptDomains；未滿足者不得自動為 Main Pick。
- **Domain Decision**：被選內容 domain 不在 `allowedConceptDomains` → 進 `DOMAIN_DECISION`，不寫任何檔，等三選一（指定既有 domain / 批准本次不產 concept note / 取消 ingest）；未決前不可部分寫入。
  - 若「批准本次不產 concept note」：concept note 步驟跳過；只寫 source note、project-link note、review-card，並更新 weekly log。
- **法文來源**：法文文章 → `raw/sources/articles/`，法文論文 → `raw/sources/papers/`；不寫 `raw/sources/french/`，不改 `new-source.mjs`；concept note 仍可落 `wiki/concepts/french/`。
- **備選處理**：兩篇備選只在 weekly log 記標題 / 連結 / 推薦理由 / 評分，不完整 ingest。
- **低分備選改選警示**：改選 A / B 且該備選任一軸 < 3 或總分明顯低於原主選時，進 SAFETY_CHECK 前顯示警示文字（「你選擇的備選低於原主選，主要弱點是：…仍可繼續，但請確認你要將它升格為本週主選。」）；已明確改選則不需第三次確認，除非同時觸發 domain / Free Access 問題。

## 寫入後

- 一律執行 `npm run kb:index`。
- strict mode：告知並取得確認後跑 `npm run kb:lint`，通過才 commit。
- quick mode：lint 可延後，但 weekly log 標 `lint_status: deferred`，且 commit 前人工確認無明顯 broken link / frontmatter 錯誤。
- commit 前先 `git status`，只 `git add` 本輪逐一指定的檔案，不 `git add -A`。
- source note 若同輪已產出 concept note 且 output / log 完成，依 `config.processedPolicy` 標 `processed: true`（concept note 內須含該 source wikilink 以通過 lint）。

## 狀態機

```
AWAITING_CONFIRMATION
  ├─ "確認主選" / "改選備選 A" / "改選備選 B"
  ▼
(改選備選且低分 → 顯示警示，不需第三次確認，繼續)
  ▼
FREE_ACCESS_CHECK
  ├─ Yes / 有免費替代版 ──► MAIN_PICK_THRESHOLD_CHECK
  └─ No / Unclear ──► ABORT（不寫任何檔，回報原因）
MAIN_PICK_THRESHOLD_CHECK
  ├─ SQ≥3 且 RV≥3 且 domain 合法 ──► DOMAIN_CHECK
  └─ 未達門檻 ──► 標「需要人工決策」，停止，等待使用者裁決
DOMAIN_CHECK
  ├─ domain ∈ allowedConceptDomains ──► SAFETY_CHECK
  └─ domain 不屬於 ──► DOMAIN_DECISION
                          ├─ ① 指定既有 domain ──► 回 SAFETY_CHECK
                          ├─ ② 批准本次不產 concept note ──► 回 SAFETY_CHECK
                          │     concept note 跳過；只寫 source / project-link / review-card + log
                          ├─ ③ 取消 ingest ──► ABORT
                          └─ 未選擇 ──► 停留 DOMAIN_DECISION（不寫任何檔）
SAFETY_CHECK（逐項見 SAFETY.md）
  ├─ 任一項未過 ──► ABORT（不寫，回報原因）
  └─ 全部通過 ──► WRITING ──► INDEX (kb:index) ──► [strict: LINT] ──► COMMIT（本輪檔案）──► DONE
```
