# 2026-W38 候選報告（使用者指定篇，降級報告）

> 產出日期：2026-09-16
> 本輪文章由使用者直接指定，跳過搜尋階段，依 `FAILURE-HANDLING.md` A 區「只有 1 篇達標」的降級報告格式處理（成因：已指定，非搜不到）。先例：2026-W31 第二篇。

## 本週主題判斷

- 預設主題：無（使用者指定）
- 選題理由：使用者 2026-09-16 指定為本週精讀
- 是否使用手動連結：是（僅此一篇）
- 是否含當週熱門內容：是。2026-09 發表，發表後數日內即有大量評論

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | We Must Pace the Frontier |
| Author | Dario Amodei（Anthropic 執行長） |
| Source | darioamodei.com 個人站 |
| URL | https://darioamodei.com/post/we-must-pace-the-frontier |
| Language | English |
| Estimated Reading Time | 約 16 分鐘 |
| Source Weight | 約 3,873 字（2026-09-16 抓取 HTML 轉純文字實測；先前工具摘要估 5,500 字有誤） |
| Type | 政策立場文（essay），非同行評審 |
| Free Access | Yes（公開頁面，HTTP 200，全文可讀） |
| Topic | AI 前沿能力的「放慢」提案：外部評估員進駐、民主國家內部協調、全球協調四級協議 |
| Domain | **需要人工 domain 決策**（見下） |

### 五軸評分

| 軸 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | 一手立場文，作者即提案者本人。未經審查，且提案內容直接影響其公司的競爭位置（利益關係明確），刻意壓低 |
| Idea Density | 4 | 論證結構清楚：兩個觸發理由、放慢後要做的四件事、三步驟、四級國際協議、checkpoint 設計。實證數據極少，多為主張 |
| Long-term Value | 3 | 政策時效性高，數月後情勢可能改變。可保值的是「放慢承諾如何被驗證」這個問題框架與四級協議的難度排序 |
| Relevance | 4 | 文中 OAI-HF 事件的 agent 攻擊評分器（grader），直接接上 vault 既有評估效度線（llm-judge-self-inconsistency、harness-induced-belief-divergence）；對寡占的批評可接 GS4455 科技與財富平權課程 |
| Obsidian Fit | 3 | 能沉澱成概念，但 domain 歸屬不乾淨，依規定降低 |
| **總分** | **17** | |

軟門檻：SQ 3 ≥ 3、Relevance 4 ≥ 3、Free Access Yes 皆成立；**domain ∈ allowedConceptDomains 未定**，故標「需要人工決策」，不得自動視為合格 Main Pick。

### Domain 問題

主題是 AI 治理與產業政策。`allowedConceptDomains` 為 ai-engineering / ai-workflow / culture-theory / french / psychology / sociology，沒有治理或政策類。可能的處理：

1. **ai-engineering**：以「安全承諾的可驗證性」為主軸，接 OAI-HF 與 Anthropic 事件報告中的評估失效機制。與既有評估效度線相接最緊，但會把文章的地緣政治與產業結構部分壓成背景。
2. **sociology**：以「在位者制定規則」與權力集中為主軸。可接 GS4455 課程，但文章本身不是社會學論證，需大量依賴批評方材料。
3. 批准本次不產 concept note。
4. 取消 ingest。

### 深度可行性

**本文單獨撐不起 6,000 字 concept note。** 3,873 字、以主張為主、幾乎沒有數據，依規格只寫本文會落入灌水。需一併回溯：

| # | 文獻 | 連結 | 厚度 | 取用狀態 | 性質 |
|---|---|---|---|---|---|
| 1 | Anthropic, Improving our alignment and security practices | https://www.anthropic.com/news/improving-alignment-security-efforts | 約 4,000 字 | HTTP 200 可讀 | 一手（文中「broken RL environments」所指事件） |
| 2 | OpenAI, The Hugging Face incident and the road ahead | https://openai.com/index/hugging-face-incident-and-the-road-ahead/ | 未知 | **curl 與 WebFetch 皆 403**，ingest 時需改用瀏覽器讀取；讀不到則只能標「未回溯原始文獻」 | 一手（OAI-HF 事件事後報告） |
| 3 | Zvi Mowshowitz, We Must Pace The Frontier | https://thezvi.substack.com/p/we-must-pace-the-frontier | 約 12,500 字 | HTTP 200 可讀 | 二手評論（安全派逐段評析） |
| 4 | Nick Mark, Pacing the Frontier, or Pacing the Narrative? | https://nickmark.substack.com/p/pacing-the-frontier-or-pacing-the | 約 1,800 字 | HTTP 200 可讀 | 二手評論（批評方） |

#1、#2 屬原始文獻回溯，符合 ingest SKILL「薄來源的處理」。#3、#4 屬多方觀點材料，**不是原始文獻**，是否可併入需使用者裁決（見「風險與限制」第 3 項）。

## Backup A / Backup B

無。本輪文章由使用者直接指定。

## 主選勝出理由

唯一候選，無比較對象。補的知識缺口：vault 既有 AI 筆記處理「評分者不穩定」「執行環境不中立」「AI 對使用者認知的作用」，沒有一篇處理「當評估本身會被模型攻擊時，外部要怎麼驗證一家公司的安全承諾」。OAI-HF 事件中 agent 試圖入侵評分器，正好是既有評估效度線推到極端的實例。

適合沉澱的概念：安全承諾的可驗證性問題；以能力門檻綁定對齊證明的 checkpoint 設計；國際協議的難度與「背叛成本」的關係。

## 風險與限制

1. **利益衝突**：作者的公司是提案受益者之一。批評方主張在位者制定的規則偏向在位者、會墊高挑戰者的成本。concept note 必須把這點當作論證的一部分處理，不能只當註腳。
2. **事件資訊多數來自二手報導**：搜尋結果中的「約 700 個 agent」「偽造日誌」等細節出自新聞與部落格，一手報告（#2）目前工具讀不到。未讀到一手前，這些數字不得寫成事實。「OpenAI 已跟進承諾」「Musk、Hassabis 表態支持」僅見於二手部落格，尚未查證。
3. **與 vault 規則的潛在衝突**：vault `CLAUDE.md` 規定 ingest 類 skill「不上網補」（例外僅 french）；weekly-reading-ingest 允許回溯原始文獻（W32 先例）。批評方評論（#3、#4）不屬原始文獻，併入需使用者明確同意。
4. **時效**：發表至今不到兩週，後續政策與各公司回應仍在變動。
5. **版權**：concept note 只能放短引文，不得大段轉錄原文。

## 建議產生的 concept note（標題草案）

- 若 ai-engineering：`ai-safety-commitment-verifiability`（AI 安全承諾的可驗證性：從評分器被攻擊到外部評估員進駐）
- 若 sociology：`frontier-ai-pacing-incumbent-rulemaking`（前沿 AI 放慢提案中的在位者制定規則問題）

## 可能的 project link

本週沒有明確專案連結。現有專案（portfolio-tracker、movie-app、personal-website、skill-portability 已完結）無一以 AI 治理為對象。skill-portability 的評估主題屬概念鄰近，不硬連。

## 使用者裁決（2026-09-16）

- Domain：**ai-engineering**（DOMAIN_DECISION ① 指定既有 domain）
- 深度規格：**本輪破例，不適用 6,000 字下限**（僅限本輪，不修改 SKILL）
- 寫作方式：照 skill 規格。先前對話中談的「論證拆解＋多方觀點對照」「中英對照」不保留
- 依上一條推定：批評方評論（#3 Zvi、#4 Nick Mark）不屬原始文獻，不併入；#1、#2 僅用於補足 OAI-HF 與 Anthropic 事件的原始出處
- 尚未收到確認語句

## 互動選項

1. 確認主選
2. 改選備選 A（本輪無）
3. 改選備選 B（本輪無）
4. 補連結後重評
5. 重新搜尋
6. 本週跳過
