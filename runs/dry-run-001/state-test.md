# State Machine Dry-Run Test｜DRY-RUN-001

> 依據 `weekly-reading-curate` / `weekly-reading-ingest` 兩份 SKILL.md 的規格，對 8 個情境進行紙上測試（不執行任何實際寫檔，不連網，不搜尋真文章）。測試基準候選報告：`candidates.md`（假資料）。

---

## 情境 1：使用者回覆「確認主選」

- **進入哪個狀態**：`AWAITING_CONFIRMATION` → `DOMAIN_CHECK`
- **是否允許寫 vault**：條件允許。`DOMAIN_CHECK` 判斷 Main Pick 草案 domain 為 `ai-engineering`，屬於 `allowedConceptDomains`，故通過 → 進 `SAFETY_CHECK` → 若 checklist 全過 → `WRITING`。
- **若不允許，原因**：不適用（本情境若 safety checklist 全部通過則允許寫）。
- **是否需要二次確認**：不需要。語句本身已是三種合法確認語句之一，且 domain 合法，不觸發 `DOMAIN_DECISION`。

## 情境 2：使用者回覆「改選備選 A」

- **進入哪個狀態**：`AWAITING_CONFIRMATION` → `DOMAIN_CHECK`（對象換成 Backup A）
- **是否允許寫 vault**：條件允許。Backup A 主題（AI agent 週報彙整）domain 草案仍可落入 `ai-engineering`，通過 `DOMAIN_CHECK` → `SAFETY_CHECK` → 若全過 → `WRITING`。
- **若不允許，原因**：不適用於本情境本身；但需注意 Backup A 的 Idea Density(2/5)、Obsidian Fit(2/5) 偏低——SKILL.md 目前**沒有**規定低分備選不可被改選為主要 ingest 對象，這是現有規格的一個空隙，僅在此記錄供日後審核，不在本輪修改規格。
- **是否需要二次確認**：不需要（除非 domain 不合法才會觸發 `DOMAIN_DECISION`，此情境未觸發）。

## 情境 3：使用者回覆「看看」

- **進入哪個狀態**：停留 `AWAITING_CONFIRMATION`（不前進）。
- **是否允許寫 vault**：不允許。
- **若不允許，原因**：「看看」不屬於 `{確認主選, 改選備選 A, 改選備選 B}` 三種合法確認語句之一；SKILL.md 明確列舉「看看/可以嗎/先放著/之後再說」不算確認。
- **是否需要二次確認**：不適用——這不是「需要二次確認」的情境，而是「尚未取得第一次有效確認」，狀態機原地等待，不會進入 `DOMAIN_CHECK` 或 `SAFETY_CHECK`。

## 情境 4：使用者回覆「本週跳過」

- **進入哪個狀態**：`SKIPPED` → `IDLE`
- **是否允許寫 vault**：不允許。
- **若不允許，原因**：v0 規格設計為「跳過」屬於明確的不 ingest 決定，不寫任何檔案（包含是否記錄到 weekly log，v0 預設不記，避免動 vault）。
- **是否需要二次確認**：不需要，「本週跳過」本身即為終態指令。

## 情境 5：被選文章無法歸入 `allowedConceptDomains`

- **進入哪個狀態**：`DOMAIN_CHECK` 失敗 → `DOMAIN_DECISION`
- **是否允許寫 vault**：不允許，且**不可部分寫入**（source / project-link / review-card / log 全部暫停）。
- **若不允許，原因**：concept domain 未決時禁止任何寫入，這是 v0 明確修正過的硬規則（避免「四類筆記只完成一部分」的不一致狀態）。
- **是否需要二次確認**：需要。只接受三選一：① 指定既有 domain（回 `SAFETY_CHECK`）② 批准本次不產 concept note（回 `SAFETY_CHECK`，但 concept 步驟整段跳過，只寫 source/project-link/review-card + log）③ 取消 ingest（`ABORT`，不寫任何檔）。未選擇前停留 `DOMAIN_DECISION`。

## 情境 6：只有 1 篇合格候選

- **進入哪個狀態**：屬於 curate 階段情境，非 ingest 狀態機的節點。`weekly-reading-curate` 會產出「降級報告」：Main Pick 正常評分，Backup 欄位寫「無達標備選」，停在 `AWAITING_CONFIRMATION`（只能選確認主選 / 補連結後重評 / 重新搜尋 / 本週跳過，「改選備選 A/B」實質上無對象）。
- **是否允許寫 vault**：在 curate 階段本身不允許（curate 從不寫 vault）；若使用者後續回「確認主選」，依情境 1 邏輯走 `DOMAIN_CHECK`/`SAFETY_CHECK` 正常判斷是否允許寫。
- **若不允許，原因**：候選數量不足不構成自動寫入或自動跳過的理由，仍需等待使用者明確指令。
- **是否需要二次確認**：候選數量不足本身不觸發二次確認；二次確認只在 domain 不合法時才出現（情境 5）。

## 情境 7：候選疑似付費牆（已修正，2026-06-22 更新）

> 原始測試發現的規格空隙已修補：`weekly-reading-ingest` SKILL.md 新增「Free Access 二次攔截」與 Safety Checklist 第二把關項，`weekly-reading-curate` SKILL.md 同步補上 Free Access 必須明確標記為 Yes/No/Unclear、Main Pick 不得為 No、原則上不得為 Unclear 的規則。

- **進入哪個狀態**：curate 階段把關（Main Pick 不得為付費牆）→ 若仍流入 ingest（curate 誤判或使用者改選到實際上付費牆的備選），進入 `FREE_ACCESS_CHECK`（新節點，位於 `DOMAIN_CHECK` 之前）。
- **是否允許寫 vault**：不允許。`FREE_ACCESS_CHECK` 判定 Free Access = No / Unclear 時直接 → `ABORT`，不寫 source note、concept note、project-link、review-card、weekly log——任何一類都不寫。
- **若不允許，原因**：curate 階段的把關不被信任為唯一防線，ingest 階段必須獨立二次攔截付費牆內容，避免「curate 失誤、ingest 照單全收」。
- **是否需要二次確認**：不需要三選一。付費牆狀態與 domain decision 性質不同——不是使用者能現場裁決補救的選擇，因此直接 `ABORT` 並回報原因，由使用者另外提供免費替代版或改選其他候選後重新觸發 ingest。

**修正後狀態機路徑**：`AWAITING_CONFIRMATION → FREE_ACCESS_CHECK →（No/Unclear）→ ABORT（不寫 vault，回報原因）`；`FREE_ACCESS_CHECK` 通過才進入原有的 `DOMAIN_CHECK → SAFETY_CHECK → WRITING` 流程。

## 情境 8：Claude routine 無法存取本機 D 槽

- **進入哪個狀態**：`CURATING`（curate 階段內的環境分支），報告完成後仍進入 `AWAITING_CONFIRMATION`，但只存在於 Claude 對話中，**不產生** `runs/YYYY-Www/candidates.md` 檔案。
- **是否允許寫 vault**：不允許，且這與 vault 無關——本情境的限制是「無法寫本機暫存檔」，不是「允許寫 vault 代替暫存」。SKILL.md 明確禁止為了保存候選而寫入 Obsidian vault。
- **若不允許，原因**：`runs/` 只是本地 Claude Code 可用時的暫存位置，非必要依賴；confirmed ingest 階段仍必須在能存取 vault 的本機環境執行，兩者環境需求不同，不可互相替代。
- **是否需要二次確認**：不需要，這純粹是輸出位置的環境分支，不影響確認語句或 domain 判斷邏輯。

---

## 測試結論

- 8 個情境中，6 個（1/2/3/4/5/6）在現有兩份 SKILL.md 規格下都有明確、可執行的處理路徑，狀態機與 safety checklist 文字足以判斷。
- 情境 7（付費牆）原本發現的規格空隙**已修補**：`weekly-reading-ingest` 新增 `FREE_ACCESS_CHECK` 節點與 Safety Checklist 第二把關項，`weekly-reading-curate` 同步補上 Free Access 標記與 Main Pick 限制規則（見上方情境 7 更新段落）。
- 情境 8（環境無法存取本機檔案）規格已覆蓋，行為符合「runs/ 非必要依賴」的設計原則。
- 情境 2（改選低分備選）原本的「額外觀察」**已修補**：`weekly-reading-ingest` 新增「低分備選改選警示」段落——不阻止使用者，但 ingest 前必須顯示警示文字；此警示不算第三次確認，除非同時觸發 domain 不合法或 Free Access 不明才需另外處理。
