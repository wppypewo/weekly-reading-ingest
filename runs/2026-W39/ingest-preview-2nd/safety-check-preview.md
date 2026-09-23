# 2026-W39 第二篇 Safety Check（PREVIEW）

執行日期：2026-09-23
模式：strict
確認語句：**確認主選**（原句「1.確認主選 2.w39 3.可以 4.不用」）

---

## 狀態機通過紀錄

| 關卡 | 結果 | 依據 |
|---|---|---|
| AWAITING_CONFIRMATION | 通過 | 使用者輸入含「確認主選」，屬三種合法語句之一 |
| FREE_ACCESS_CHECK | 通過 | Open Access，CC BY 4.0，頁面標 `isAccessibleForFree: true`，HTTP 200，全文已讀 |
| MAIN_PICK_THRESHOLD_CHECK | 通過 | SQ 5 ≥ 3、RV 4 ≥ 3、Free Access = Yes |
| DOMAIN_CHECK | 通過 | human-sciences ∈ allowedConceptDomains，不需 DOMAIN_DECISION |
| 低分備選警示 | 不適用 | 確認主選，非改選 |
| DEPTH_CHECK | 通過 | 見下方實測 |

---

## Safety Checklist 逐項

```
[x] 確認語句屬於 {確認主選, 改選備選 A, 改選備選 B} 之一 → 「確認主選」
[x] 對應週候選內容存在 → runs/2026-W39/candidates-2nd-pick.md（不覆寫第一篇的 candidates.md）
[x] 候選報告含評分與主選理由 → 五軸評分 + 勝出理由 + 風險限制 + 使用者裁決紀錄
[x] 低分備選警示 → 不適用（非改選）
[x] Free Access = Yes → HTML 全文已讀
[x] Main Pick 軟門檻 → SQ 5 / RV 4 / Free Yes / domain 合法
[x] concept domain ∈ allowedConceptDomains → human-sciences ✓
[x] 二次確認 → 使用者已明確指定週次、回溯範圍與課程頁處理方式（2026-09-23）
[x] source 寫入範圍僅限 raw/sources/<articles|papers|videos|books>/ → papers（目錄已存在）
[x] 寫入範圍僅限 SAFETY.md 允許路徑 → 見下方寫入清單
[x] project-link frontmatter → 本輪不產 project-link
[x] source 正文不改寫；無備選 → 已遵守，source note 為繁中重寫摘要，無長段引文
[x] 不改 meta/index.md、meta/log.md、meta/lint.md；不動 wiki/projects/
[ ] commit 前執行 git status → 待寫入後、commit 前執行（commit 需你另外指示）
[x] 候選報告留在 runs/，不複製進 vault
[x] 不自動 commit、不自動 push
```

---

## DEPTH_CHECK 實測

| 檢查項 | 實測 |
|---|---|
| concept 字數 | 23,924（`wc -m`，扣 preview 標頭、frontmatter、末尾相關概念清單；寫入 vault 後重量） |
| source 字數 | 9,669（扣 preview 標頭、frontmatter） |
| concept ≥ source | 成立 |
| 6,000 字下限 | 成立 |
| 章節覆蓋 | 核心結論 ✅／背後原因・機制 ✅（8 小節）／使用場景 ✅／容易混淆 ✅／常見陷阱 ✅／與專案關係 ✅／來源 ✅／未確認・待查證 ✅／相關概念 ✅ |
| 補入的原始文獻 | *Social capital II*（*Nature* 608, 122–134）全文，標 `[外部 SC2]`，已登記 `external_sources` |
| 反 AI 味檢查 | `——` 0 處；粗體全篇 1 處（核心結論）；中文禁用詞掃描 0 筆 |
| 連結檢查 | concept 內 5 個 wikilink：4 個指向既有檔案，1 個指向本輪新增的 source note |

---

## 本輪寫入清單

| 路徑 | 動作 | 說明 |
|---|---|---|
| `raw/sources/papers/2026-W39-social-capital-economic-connectedness.md` | 新增 | 無檔名衝突 |
| `wiki/concepts/human-sciences/economic-connectedness-bridging-social-capital.md` | 新增 | 無檔名衝突；目錄已存在 |
| `meta/weekly-reading/log.md` | 追加 | 只在檔尾既有 `## 2026-W39` 區塊之後新增 `### 本週第二篇` 子節 |

寫入後：`npm run kb:index` 會更新 `meta/index.md`（腳本產物）。

**不產**：project-link（現有專案皆為技術性專案）、review card（2026-08-01 起停產）。

**不修改**：GS4455 課程 hub 頁（依你的裁決第 4 點）；human-sciences 既有頁不加反向連結。

---

## 需要你知道的事

### 1. 影片的說法與論文不符

截圖字幕「跳出群體共識才配有超額財富」「要取得遠超同齡人的財富體量」在論文裡找不到對應。結果變數是低所得家庭子女約 35 歲時的所得百分位，比較單位是郡與郵遞區號。論文中最接近「群體」的網絡凝聚，結論是與流動沒有穩定關係。兩份筆記都記下了這個對照。

### 2. 「所得增加約 20%」是推算

摘要裡的 20% 是把 Chetty & Hendren 的地區因果效果（EC 高 1 單位 → 所得 +30.7%）乘上低、高 SES 孩子的 EC 差 0.636，得到 19.5%。作者自己說 EC 本身的因果效果沒有識別。concept note 照這個強度寫，沒有寫成「交到高 SES 朋友會讓所得增加 20%」。

### 3. SC2 的回溯範圍

讀的是主文與 Methods。用到的部分是 EC 拆成「接觸機會」與「交友偏誤」的分解、高中與大學的例子、作者列舉的三個具名介入實例。這些實例作者都沒有評估效果，concept note 寫明了這一點。修正了兩處措辭，讓強度對齊原文：Wayne State 與 Howard 那句原本寫「差異主要來自 bias」，原文只說差異相當大、來自 bias 的不同；健身房例子的「時薪 20–60 美元」註明是教練的收入。

### 4. 課程頁有一句過時描述，沒改

GS4455 hub 頁「與既有筆記的接點」寫 human-sciences 只有一篇，本輪寫入後也不準確。依你的裁決不動課程頁；要更新的話需要你另外指示。

---

**下一步：寫入 vault → 重量字數 → `npm run kb:index` → 告知後跑 `kb:lint` → commit 等你另外指示。**
