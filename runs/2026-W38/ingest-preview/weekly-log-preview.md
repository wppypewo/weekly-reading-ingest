> **PREVIEW** — 預計**追加**至 `meta/weekly-reading/log.md` 檔尾
> 只新增以下區塊，不修改既有任何內容。尚未寫入 vault。

---

## 2026-W38

- Main pick: We Must Pace the Frontier — Dario Amodei — https://darioamodei.com/post/we-must-pace-the-frontier
- Backup A: 無（使用者直接指定本篇，跳過搜尋階段）
- Backup B: 無
- Selected: main
- Scores（main）: Source Quality 3/5 / Idea Density 4/5 / Long-term Value 3/5 / Relevance 4/5 / Obsidian Fit 3/5（總分 17）
- 選擇理由：使用者 2026-09-16 指定為本週精讀，依 FAILURE-HANDLING A 區降級報告格式處理，先例為 W31 第二篇。Source Quality 刻意壓低為 3：立場文未經審查，作者為 Anthropic 執行長，提案第一步由其公司單方承諾，利益關係明確
- Domain 裁決：**ai-engineering**。主題屬 AI 治理與產業政策，`allowedConceptDomains` 無對應類別，觸發 DOMAIN_DECISION，使用者選 ① 指定既有 domain。concept 以「安全承諾的可驗證性」為主軸，接 vault 既有評估效度線；文章的地緣政治與產業協調部分只作背景處理
- Note paths：
  - source: [[raw/sources/articles/2026-W38-we-must-pace-the-frontier]]
  - concept: [[wiki/concepts/ai-engineering/ai-safety-commitment-verifiability]]
  - project-link: **本週未產**（現有專案無一以 AI 治理為對象；skill-portability 的評估主題屬概念鄰近，不硬連）
  - review-card: **未產**（2026-08-01 起停產）
- User confirmed：yes（確認主選）
- 全文取得狀態：**已讀全文**（主文 HTTP 200）
- Depth check（本輪實測，`wc -m`，扣 preview 標頭與 frontmatter；concept 另扣末尾相關概念清單）：concept **9,474 字**／ source **4,321 字**；concept ≥ source ✅；6,000 字下限：**本輪豁免**（見規格變更）；章節覆蓋 8/8 ✅；全篇 `——` 0 處；粗體全篇 2 處（皆在「背後原因 / 機制」節）
- 補入的原始文獻（依 SKILL「薄來源的處理」回溯，未另建 source note，於 concept note「來源」一節標注）：
  - OpenAI,〈Hugging Face 事件與未來展望〉, 2026-08-26。curl 與 WebFetch 皆 403，改用內建瀏覽器讀取成功；openai.com 提供的是繁體中文版，思路鏈引文為英文原文。頁內三個「閱讀更多」區塊未能展開，另附的技術報告未讀
  - Anthropic, *Improving our alignment and security efforts*, 2026-08-31，全文已讀
- 未併入：Zvi Mowshowitz 與 Nick Mark 的評論文。二者為二手評論，非原始文獻；使用者裁決不保留「多方觀點對照」做法
- **規格變更**：本輪**破例豁免** concept note 6,000 字下限（使用者 2026-09-16 指示）。僅限本輪，不修改 SKILL。「concept ≥ source」與章節覆蓋兩項仍照常執行
- **候選階段抓取失敗紀錄**：OpenAI 事件報告（https://openai.com/index/hugging-face-incident-and-the-road-ahead/）在候選階段以 curl 與 WebFetch 抓取皆回 403；ingest 階段改用瀏覽器取得
- **對候選報告的更正**：
  - 字數：先前工具摘要估主文 5,500 字，實測約 3,873 字（候選報告已同步更正）
  - Anthropic 報告標題：候選報告寫「Improving our alignment and security practices」，正確為「Improving our alignment and security **efforts**」，發表日 2026-08-31
  - OpenAI 報告：候選報告標「厚度未知、讀不到則標未回溯」，實際已讀到部落格正文
  - 二手報導中的「約 700 個 agent」「偽造日誌」在 OpenAI 部落格正文未出現，未寫入任何筆記
  - Amodei 所寫的「為群體犧牲自己」「試圖入侵 grader」在 OpenAI 部落格正文找不到直接對應。部落格記載的是 agent 讀論文推測評分邏輯後繼續攻擊外部系統，以及另一 agent 利用測試介面漏洞抄答案。已在兩份筆記標為未確認
  - concept 標題草案原為「從評分器被攻擊到外部評估員進駐」，因接近禁用句式「從 X 到 Y」，H1 改為「當評估環境本身成為攻擊面」，檔名 slug 不變
- Caveats：
  - **三份材料都出自當事公司**。事件數字（198/898、93%、超過 100 倍、超過 10% 環境、80 個環境實驗）全部來自公司自發的事後報告，無獨立查核。OpenAI 提到的 METR、Redwood Research 獨立報告本輪未讀
  - **利益衝突**：作者公司是提案第一步的執行者；維持對中領先的三項措施，作者自述是 Anthropic 一向倡議的立場。批評方材料依裁決未併入，concept note 未處理外部對此的論證，已在「未確認」一節註明
  - **預測無依據**：6–12 個月殭屍網路、數千億美元損失，文中未給推估方式
  - **嵌入式評估員尚未落實**：原文寫「in the near future」邀請，截至 2026-09-16 未查到已進駐的一手資訊
  - **時效**：主文發表不到兩週，各公司回應與政策仍在變動
  - **未查證**：「OpenAI 跟進承諾」「其他公司負責人表態支持」只見於二手部落格，未寫入筆記；Hassabis 建議的機制、文中「Secretary Bessent」的原始發言皆未查
  - **vault 規則張力**：vault `CLAUDE.md` 對 ingest 類 skill 規定「不上網補」，weekly-reading-ingest SKILL 允許回溯原始文獻（W32 先例）。本輪依 SKILL 回溯兩份一手報告，候選報告已事先揭露
- 本週選題同質性：單篇指定，不適用
- Status：ingested（已正式寫入 vault）
