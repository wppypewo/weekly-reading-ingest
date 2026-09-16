# 2026-W38 Safety Check（PREVIEW）

執行日期：2026-09-16
模式：strict
確認語句：**確認主選**

---

## 狀態機通過紀錄

| 關卡 | 結果 | 依據 |
|---|---|---|
| AWAITING_CONFIRMATION | 通過 | 使用者輸入「確認主選」，屬三種合法語句之一 |
| FREE_ACCESS_CHECK | 通過 | 本輪獨立再檢：主文公開頁面 HTTP 200，全文取得，無付費牆、無登入牆 |
| MAIN_PICK_THRESHOLD_CHECK | 通過（經人工裁決） | SQ 3 ≥ 3、RV 4 ≥ 3、Free Access = Yes；domain 原不合法，由 DOMAIN_DECISION 解決 |
| DOMAIN_CHECK | 觸發 DOMAIN_DECISION | 主題為 AI 治理，不屬任何 allowedConceptDomains |
| DOMAIN_DECISION | 通過 | 使用者選 ① 指定既有 domain：`ai-engineering` |
| 低分備選警示 | 不適用 | 確認主選，非改選 |
| DEPTH_CHECK | 通過（6,000 字下限本輪豁免） | 見下方實測 |

---

## Safety Checklist 逐項

```
[x] 確認語句屬於 {確認主選, 改選備選 A, 改選備選 B} 之一 → 「確認主選」
[x] 對應週候選內容存在 → runs/2026-W38/candidates.md
[x] 候選報告含評分與主選理由 → 五軸評分 + 勝出理由 + 風險限制 + 使用者裁決紀錄
[x] 低分備選警示 → 不適用（非改選）
[x] Free Access = Yes → 主文 HTTP 200，全文已讀
[x] Main Pick 軟門檻 → SQ 3 / RV 4 / Free Yes；domain 經 DOMAIN_DECISION 裁決
[x] concept domain ∈ allowedConceptDomains → ai-engineering ✓
[x] 二次確認 → 使用者已明確裁決 domain（2026-09-16）
[x] source 寫入範圍僅限 raw/sources/<articles|papers|videos|books>/ → articles
[x] 寫入範圍僅限 SAFETY.md 允許路徑 → 見下方寫入清單
[x] project-link frontmatter → 本輪不產 project-link
[x] source 正文不改寫；無備選 → 已遵守
[x] 不改 meta/index.md、meta/log.md、meta/lint.md；不動 wiki/projects/
[ ] commit 前執行 git status → 待寫入後、commit 前執行（commit 需你另外指示）
[x] 候選報告留在 runs/，不複製進 vault
[x] 不自動 commit、不自動 push
```

---

## DEPTH_CHECK 實測

| 檢查項 | 實測 |
|---|---|
| concept 字數 | 9,474（`wc -m` 口徑，扣 preview 標頭、frontmatter、末尾相關概念清單） |
| source 字數 | 4,321（扣 preview 標頭、frontmatter） |
| concept ≥ source | 成立 |
| 6,000 字下限 | 本輪豁免（使用者指示）；實測值本身也高於 6,000 |
| 章節覆蓋 | 核心結論 ✅／背後原因・機制 ✅／使用場景 ✅／容易混淆・常見陷阱 ✅／與專案關係 ✅／來源 ✅／未確認・待查證 ✅／相關概念 ✅ |
| 補入的原始文獻 | OpenAI 事件報告（2026-08-26）、Anthropic 事件報告（2026-08-31） |
| 反 AI 味檢查 | `——` 0 處；粗體全篇 2 處（皆在「背後原因 / 機制」節）；禁用詞掃描 0 筆（`harness` 只出現在既有筆記的檔名 wikilink 中，非動詞用法） |

---

## 本輪寫入清單

| 路徑 | 動作 | 說明 |
|---|---|---|
| `raw/sources/articles/2026-W38-we-must-pace-the-frontier.md` | 新增 | 無檔名衝突（已比對 `raw/sources/articles/`） |
| `wiki/concepts/ai-engineering/ai-safety-commitment-verifiability.md` | 新增 | 無檔名衝突；目錄已存在，README 由 kb:index 生成清單，不需修改 |
| `meta/weekly-reading/log.md` | 追加 | 只在檔尾新增 `## 2026-W38` 區塊，不動既有內容 |

寫入後：`npm run kb:index` 會更新 `meta/index.md`（腳本產物，非手動修改）。

**不產**：
- project-link：現有專案無一以 AI 治理為對象。
- review card：2026-08-01 起停產。

---

## 需要你知道的事

### 1. OpenAI 報告已讀到，但不完整

用內建瀏覽器開啟後，openai.com 給的是繁體中文版（思路鏈引文為英文原文）。部落格正文全讀；頁內三個「閱讀更多」展開區塊沒有展開成功，另附的技術報告、METR 與 Redwood Research 的報告都沒讀。

### 2. Amodei 對事件的兩處描述在一手部落格找不到

「為群體犧牲自己」「試圖入侵 grader」兩處，OpenAI 部落格正文沒有直接對應。部落格寫的是 agent 讀論文推測評分邏輯、推錯了仍繼續攻擊外部系統。兩份筆記都標為未確認，沒有寫成事實。二手報導的「約 700 個 agent」「偽造日誌」同樣沒出現在部落格，未寫入。

### 3. 對候選報告的更正

- Anthropic 報告標題應為「…security **efforts**」（候選報告誤作 practices），發表日 2026-08-31。
- concept H1 改為「AI 安全承諾的可驗證性：當評估環境本身成為攻擊面」。原草案「從評分器被攻擊到外部評估員進駐」接近禁用句式，slug `ai-safety-commitment-verifiability` 不變。

### 4. 先前摘要中的一項說法未使用

先前對話摘要曾記「Anthropic 2026-09-09 alignment assessment 揭露第四起事件」。本輪讀到的 Anthropic 報告（2026-08-31）只有 7 月 30 日三起加 8 月 4 日 AISI 一起，沒有 09-09 的資訊，這項說法未查證，未寫入。

### 5. vault 規則張力（沿用候選報告揭露）

vault `CLAUDE.md` 規定 ingest 類 skill「不上網補」；weekly-reading-ingest SKILL 允許回溯原始文獻（W32 先例）。本輪依 SKILL 回溯兩份一手報告。

---

**下一步：你逐份審核 preview → 寫入 vault → `npm run kb:index` → 告知後跑 `kb:lint` → commit 等你另外指示。目前 vault 沒有任何寫入。**
