# 2026-W33 Safety Check（PREVIEW）

執行日期：2026-08-16
模式：strict
確認語句：**確認主選**

---

## 狀態機通過紀錄

| 關卡 | 結果 | 依據 |
|---|---|---|
| AWAITING_CONFIRMATION | 通過 | 使用者輸入「確認主選」，屬三種合法語句之一 |
| FREE_ACCESS_CHECK | 通過 | Frontiers 全開放取用，本輪獨立再檢：對同一 URL 實際抓取三次全部成功取得全文，無付費牆、無登入牆、無 redirect 阻擋 |
| MAIN_PICK_THRESHOLD_CHECK | 通過 | Source Quality 3 ≥ 3、Relevance 4 ≥ 3、Free Access = Yes、domain 合法 |
| DOMAIN_CHECK | 通過 | `sociology` ∈ `allowedConceptDomains`，未觸發 DOMAIN_DECISION |
| 低分備選警示 | 不適用 | 本輪為確認主選，非改選備選 |

---

## Safety Checklist 逐項

```
[x] 確認語句屬於 {確認主選, 改選備選 A, 改選備選 B} 之一 → 「確認主選」
[x] 對應週候選內容存在 → runs/2026-W33/candidates.md
[x] 候選報告含評分與主選理由 → 三篇五軸評分 + 勝出理由 + 風險限制齊備
[x] 低分備選警示 → 不適用（非改選）
[x] Free Access = Yes → Frontiers 開放取用，全文三次抓取皆成功
[x] Main Pick 軟門檻 → SQ 3 / RV 4 / Free Yes / domain 合法，四項全過
[x] concept domain ∈ allowedConceptDomains → sociology ✓
[x] 二次確認 → 不適用（未觸發 DOMAIN_DECISION）
[x] source 寫入範圍僅限 raw/sources/<articles|papers|videos|books>/ → papers
[x] 寫入範圍僅限 SAFETY.md 五類路徑 → 見下方寫入清單
[x] project-link frontmatter → 本輪不產 project-link
[x] source 正文不改寫；備選只存標題/連結/理由/評分 → 已遵守
[x] 不改 meta/index.md、meta/log.md、meta/lint.md；不改 tools/kb/*.mjs；不動 wiki/projects/
[x] commit 前已執行 git status → 工作區乾淨，無其他未提交變更
[x] 候選報告留在 runs/，不複製進 vault
[x] 不自動 commit、不自動 push
```

---

## 本輪寫入清單

| 路徑 | 動作 | 說明 |
|---|---|---|
| `raw/sources/papers/2026-W33-ai-intimacy-youtube-discourse.md` | 新增 | 無檔名衝突（已比對 `raw/sources/papers/`） |
| `wiki/concepts/sociology/` | **新增目錄** | 見下方說明 |
| `wiki/concepts/sociology/README.md` | 新增 | 比照 `wiki/concepts/psychology/README.md` 格式 |
| `wiki/concepts/sociology/ai-intimacy-recognition-extraction-double-bind.md` | 新增 | 無檔名衝突 |
| `meta/weekly-reading/log.md` | 追加 | 只在檔尾新增 `## 2026-W33` 區塊，不動既有內容 |

**不產**：
- project-link — 五個專案（robot-check、rot、portfolio-tracker、movie-app、personal-website）無一以親密關係或社會學為對象。robot-check 的「證明你不是機器人」與本篇的「與機器人建立親密關係」之間只有修辭鄰近，不是概念關聯，依規定不硬連。
- review card — 2026-08-01 起停產。

---

## 需要你知道的兩件事

### 1. 新增 `wiki/concepts/sociology/` 目錄

`sociology` 於 2026-07-31 加入 `allowedConceptDomains`，但目錄至今不存在（依 2026-06-28「不預先建立空白領域資料夾」決策，有筆記時才建）。本輪是該 domain 的第一篇，因此需要建立目錄與 README。

此路徑在 `SAFETY.md` 的允許寫入範圍內（`wiki/concepts/<allowedConceptDomains 之一>/`）。SAFETY.md 要求事前確認的是 `wiki/outputs/weekly-reading/` 與 `meta/weekly-reading/`，兩者皆已存在。仍在此明示，因為這是本輪唯一的新目錄。

### 2. 一項對候選報告的更正

候選報告的「風險與限制」第 2 項寫「引文經作者改寫以匿名化⋯⋯報告中所有留言引文都不是逐字原文」。**這是錯的，範圍寫太寬。**

原文的倫理聲明是：所有可識別資訊已移除，其中 **四則**引文經「lightly modified」以去除具辨識度的個人細節並保留原意。也就是說絕大多數引文為逐字原文，只有四則經輕度改寫。

已在 source note 與 concept note 依原文正確記錄。此更正不影響主選判斷，也不改變任何評分。

---

## 授權標示的處理

Frontiers 為開放取用出版商，本文全文無任何取用限制，Free Access 判定為 Yes 無疑義。

但三次抓取皆未取得該文授權聲明的**逐字原文**（頁面該區塊未進入抓取內容）。因此 source note 記為「Frontiers 開放取用；CC BY 授權未逐字確認」，不寫成已確認的 CC BY 4.0。此為誠實標示，不影響 Free Access 通關。

---

**下一步：WRITING → DEPTH_CHECK → INDEX → LINT → COMMIT。preview 尚未寫入 vault。**
