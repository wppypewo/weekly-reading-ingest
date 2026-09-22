---
name: weekly-reading-curate
description: 每週精讀策展——搜尋候選、評分、產出 1 主選 + 2 備選報告。當使用者說「本週精讀」「weekly reading curate」「找本週候選」「/weekly-reading-curate」時觸發，或由 Claude routine 每週六 10:00 呼叫。只產報告，不寫 vault。
---

# weekly-reading-curate

每週精讀策展的「搜尋 + 評分 + 產報告」階段。**不寫入 Obsidian vault**，只負責產出候選報告供使用者確認。

## 執行前必讀

- [`FAILURE-HANDLING.md`](../../../FAILURE-HANDLING.md)：候選階段失敗情境（抓不到全文、來源連不上、candidates 同週重跑等）。
- [`MODES.md`](../../../MODES.md)：strict / quick 模式（curate 兩模式皆須產候選報告 + 人工確認）。
- 路徑與白名單一律以工具專案根目錄的 `weekly-reading.config.json` 為準，不在本檔散落絕對路徑。

## 職責

1. 讀取 `weekly-reading.config.json`（`vaultRoot`、`allowedConceptDomains`、`allowedSourceFolders`、`weeklyPickCount`、`freeOnly` 等）。
2. 讀取必要的 vault context（只讀，不寫）：
   - `schema/context/current-focus`
   - `wiki/projects/*/current-status`
3. 根據使用者近期專案、興趣、知識缺口決定本週候選方向；預設由 Claude 判斷，但：
   - 支援使用者手動指定主題
   - 支援使用者排除特定主題
   - 支援使用者提供手動連結，與自動搜尋結果混合評分，不因「使用者提供」而加分
4. 搜尋候選（只收免費可讀內容；付費牆不得作為主選）。Free Access 規則：
   - 每篇候選的 Free Access 欄位必須在候選報告中明確標記為 `Yes` / `No` / `Unclear` 三者之一，不得留白或模糊敘述。
   - Main Pick 的 Free Access 必須是 `Yes`，或有明確免費替代版（例如 arXiv、作者 PDF、官方開放版），並在報告中寫出該替代版的來源。
   - Free Access = `No` **不得**列為 Main Pick。
   - Free Access = `Unclear` 原則上**不得**列為 Main Pick，除非報告明確說明免費替代版；無法說明則只能列為備選或剔除。
   - 若沒有足夠免費候選，不要硬湊——可以少於 1 主選 + 2 備選，或回報「本週無合格候選」。
5. 對每篇候選評五項分數（見下方候選報告格式），評分須有區分度，不得全部給 4 或 5。
6. 判斷主選：
   - 不只看總分，需在報告中說明勝出理由、補的知識缺口、適合沉澱的概念、可能的專案連結、限制與風險。
   - **Main Pick 軟門檻**（對應 `config.mainPickThreshold`）：原則上必須同時滿足 `Source Quality ≥ 3`、`Relevance ≥ 3`、`Free Access = Yes`、`domain ∈ allowedConceptDomains`。候選非常特殊但未滿足上述條件時，**不得自動列為 Main Pick**，必須標記「需要人工決策」。此為軟門檻，不引入額外公式、不改五軸評分。
   - 主選原則上必須能歸入 `allowedConceptDomains` 之一；若全週最高品質候選無法歸入，不得自動列為主選，改列為備選並標記「需要人工 domain 決策」，且該篇 Obsidian Fit 評分需降低。
   - **深度可行性評估**（2026-07-31 新增）：ingest 階段的 concept note 有 6,000 字硬性下限（見 `weekly-reading-ingest` SKILL 的「concept note 深度規格」）。**來源本身不設厚度門檻**——薄來源可以選——但主選必須在報告中回答「這個來源撐不撐得起 6,000 字」：
     - 撐得起：說明理由（頁數／論證數量／數據量）。
     - 撐不起：**必須在報告中列出要一併回溯的原始文獻清單**（標題 + 連結 + 厚度），作為主選的一部分。缺這份清單的薄來源不得列為 Main Pick。
     - 嚴禁以「ingest 時再想辦法湊字數」帶過。字數是靠補材料達成，不是靠灌水達成。
7. 產出候選報告（格式見下方），輸出到 Claude 界面。
8. 若本地 Claude Code 可存取檔案，**另外**存一份到 `runs/YYYY-Www/candidates.md`；若執行環境無法存取本機檔案（例如 routine 在無檔案系統存取權的環境執行），報告只留在 Claude 界面對話中，不視為失敗，也不嘗試用任何方式寫入 Obsidian vault 來代替保存。

## 嚴禁

- 不得寫入 Obsidian vault 任何路徑。
- 不得建立 source / concept / project-link / review-card 筆記。
- 不得改 `meta/index.md`、`meta/log.md`、`meta/lint.md`。
- 不得改 `tools/kb/*.mjs`。
- 不得改 `wiki/projects/` 下任何檔案。
- 不得把候選報告寫進 vault（任何路徑都不行）。
- 不得因總分最高就自動決定主選（需有區分度的理由說明）。
- 不得推薦付費牆內容作為主選。
- 不得用低品質文章湊滿 1 主選 + 2 備選——候選不足時寧可少於 3 篇或回報「本週無合格候選」。

## 候選報告格式

必須包含：

- 本週主題判斷（預設主題 / 選題理由 / 是否使用手動連結 / 是否含當週熱門內容）
- Main Pick（含 Title / Author / Source / URL / Language / Estimated Reading Time / **Source Weight** / Type / Free Access / Topic）
  - **Source Weight**：論文標頁數，非論文標估計字數。不得留白，不得寫「未知」而不說明取得失敗的原因。
  - 主選另需「深度可行性」欄位：撐得起 6,000 字 concept note 的理由，或要一併回溯的原始文獻清單。
- Backup A（同上欄位 + 推薦理由）
- Backup B（同上欄位 + 推薦理由）
- 每篇五項評分：
  - Source Quality (1–5)
  - Idea Density (1–5)
  - Long-term Value (1–5)
  - Relevance (1–5)
  - Obsidian Fit (1–5)
- 主選勝出理由（為何是主選、為何勝過兩備選、補的知識缺口、適合沉澱的概念、可能的專案連結）
- 風險與限制
- 建議產生的 concept note（標題草案）
- 可能的 project link（無明確關聯則寫「本週沒有明確專案連結」，不硬連）
- 互動選項（固定六項）：
  1. 確認主選
  2. 改選備選 A
  3. 改選備選 B
  4. 補連結後重評
  5. 重新搜尋
  6. 本週跳過

## 結束狀態

報告產出後進入「等待確認」，不自動觸發 `weekly-reading-ingest`。
