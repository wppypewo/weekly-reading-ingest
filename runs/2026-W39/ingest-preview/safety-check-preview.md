# 2026-W39 Safety Check（PREVIEW）

執行日期：2026-09-21
模式：strict
確認語句：**確認主選**（原句「確認主選，domain 用 ai-workflow，回溯 METR 研究」）

---

## 狀態機通過紀錄

| 關卡 | 結果 | 依據 |
|---|---|---|
| AWAITING_CONFIRMATION | 通過 | 使用者輸入含「確認主選」，屬三種合法語句之一 |
| FREE_ACCESS_CHECK | 通過 | 本輪獨立再檢：官方逐字稿頁 HTTP 200，`isAccessibleForFree: true`，全文取得；影片公開 |
| MAIN_PICK_THRESHOLD_CHECK | 通過 | SQ 3 ≥ 3、RV 4 ≥ 3、Free Access = Yes；domain 由使用者指定為 ai-workflow |
| DOMAIN_CHECK | 通過 | ai-workflow ∈ allowedConceptDomains，不需 DOMAIN_DECISION |
| 低分備選警示 | 不適用 | 確認主選，非改選 |
| DEPTH_CHECK | 通過 | 見下方實測 |

---

## Safety Checklist 逐項

```
[x] 確認語句屬於 {確認主選, 改選備選 A, 改選備選 B} 之一 → 「確認主選」
[x] 對應週候選內容存在 → runs/2026-W39/candidates.md
[x] 候選報告含評分與主選理由 → 五軸評分 + 勝出理由 + 風險限制 + 使用者裁決紀錄
[x] 低分備選警示 → 不適用（非改選）
[x] Free Access = Yes → 逐字稿 HTTP 200，全文已讀
[x] Main Pick 軟門檻 → SQ 3 / RV 4 / Free Yes / domain 合法
[x] concept domain ∈ allowedConceptDomains → ai-workflow ✓
[x] 二次確認 → 使用者已明確指定 domain 與回溯範圍（2026-09-21）
[x] source 寫入範圍僅限 raw/sources/<articles|papers|videos|books>/ → videos（目錄尚不存在，寫入時新建；config allowedSourceFolders 含 videos）
[x] 寫入範圍僅限 SAFETY.md 允許路徑 → 見下方寫入清單
[x] project-link frontmatter → 本輪不產 project-link
[x] source 正文不改寫；無備選 → 已遵守，source note 只作摘要，引文為短句
[x] 不改 meta/index.md、meta/log.md、meta/lint.md；不動 wiki/projects/
[ ] commit 前執行 git status → 待寫入後、commit 前執行（commit 需你另外指示）
[x] 候選報告留在 runs/，不複製進 vault
[x] 不自動 commit、不自動 push
```

---

## DEPTH_CHECK 實測

| 檢查項 | 實測 |
|---|---|
| concept 字數 | 18,864（`wc -m`，扣 preview 標頭、frontmatter、末尾相關概念清單；寫入 vault 後重量） |
| source 字數 | 5,253（扣 preview 標頭、frontmatter） |
| concept ≥ source | 成立 |
| 6,000 字下限 | 成立 |
| 章節覆蓋 | 核心結論 ✅／背後原因・機制 ✅（8 小節）／使用場景 ✅／容易混淆 ✅／常見陷阱 ✅／與專案關係 ✅／來源 ✅／未確認・待查證 ✅／相關概念 ✅ |
| 補入的原始文獻 | METR 2025-07-10 部落格與 arXiv 2507.09089 全文；METR 2026-02-24 更新全文 |
| 反 AI 味檢查 | `——` 0 處；粗體全篇 2 處（核心結論 1、機制節表格 1）；中文禁用詞掃描 0 筆（「從 X 到 Y」命中皆為數值區間） |

---

## 本輪寫入清單

| 路徑 | 動作 | 說明 |
|---|---|---|
| `raw/sources/videos/2026-W39-dario-amodei-end-of-exponential.md` | 新增 | `videos/` 目錄新建；無檔名衝突 |
| `wiki/concepts/ai-workflow/coding-automation-spectrum.md` | 新增 | 無檔名衝突；目錄已存在 |
| `meta/weekly-reading/log.md` | 追加 | 只在檔尾新增 `## 2026-W39` 區塊 |

寫入後：`npm run kb:index` 會更新 `meta/index.md`（腳本產物）。

**不產**：project-link（現有專案無一以開發生產力量測為對象）、review card（2026-08-01 起停產）。

**不修改**：既有 [[wiki/concepts/ai-workflow/coding-agent-productivity-proxy-gap]] 不加反向連結，避免改動範圍外檔案。要不要補反向連結由你決定。

---

## 需要你知道的事

### 1. Dwarkesh 對 METR 研究的描述不準

他說研究看的是「合併回去的產出」。原文量的是開發者自報的完成時間，並說兩組 PR 品質在質性上相近。數字（20% vs. 19%）接近，量測對象不同。concept note 已寫明。

### 2. 訪談比 METR 的後續更新早 11 天

訪談 2026-02-13，METR 2026-02-24 發布更新，說新實驗因選擇效應量不準，初步估計轉為加速（−18%、−4%），但自評不可靠。concept note 兩份並列，沒有畫成趨勢。

### 3. 對候選報告的一項更正

候選報告更正過程中，我把「持續學習 1–2 年內解決」判為 Dwarkesh 的轉述而刪除。今天重讀逐字稿，Amodei 本人確實說「a good chance that in the next year or two」會解決。候選報告現行版本沒有此項，不影響評分；source note 已照原文寫入。

### 4. 未回溯

〈The Adolescence of Technology〉與 Claude constitution 公告，依你的指示不抓，列在未確認。METR 2026 年 5 月問卷只見摘要，未寫入正文。

---

**下一步：你審核 preview → 寫入 vault → `npm run kb:index` → 告知後跑 `kb:lint` → commit 等你另外指示。目前 vault 沒有任何寫入。**
