# Ingest Preview（quick mode, 合併）— Backup A：Rating Roulette

> 本週第二篇（W26 已有首篇）。quick mode 合併預覽；確認後才寫入 vault。論文 → `raw/sources/papers/`，domain `ai-engineering`。
> 限制：僅依 arXiv abstract 與 WebFetch 結構摘要，未精讀 19 頁全文 → confidence: medium，caveat 明寫。

## 將寫入的檔案

```
raw/sources/papers/2026-W26-rating-roulette-llm-judge-self-inconsistency.md
wiki/concepts/ai-engineering/llm-judge-self-inconsistency.md
wiki/outputs/weekly-reading/project-links/2026-W26-rating-roulette-llm-judge-self-inconsistency.md
wiki/outputs/weekly-reading/review-cards/2026-W26-rating-roulette-llm-judge-self-inconsistency.md
meta/weekly-reading/log.md（在 W26 段落增列第二篇）
```

## 1. Source note（papers）要點

- type: source / domain: ai-engineering / processed: 先 false，ingest 後依 policy 設 true（concept 回連）/ confidence: medium / tags: [weekly-reading]
- Title: Rating Roulette: Self-Inconsistency in LLM-As-A-Judge Frameworks
- Author: Haldar & Hockenmaier（arXiv 2510.27106, CC BY 4.0）
- 短節錄（引用線索）：self-inconsistency 指 LLM 評分器對「相同輸入」重複評估會出現顯著變異。
- 繁中摘要（重寫）：論文跨多模型（Claude / DeepSeek-R1 / Qwen）檢視 LLM-as-a-Judge 的自我不一致性，用 Cohen's / Fleiss' Kappa 量化評判一致性，指出單次評分不可假設穩定；偏診斷與量測，緩解建議較少。
- Caveats：僅依 abstract 與結構摘要、未精讀全文；preprint 未經同行評審；偏問題診斷少可操作解法。

## 2. Concept note（ai-engineering）

- 檔名：`llm-judge-self-inconsistency`
- 核心結論：把 LLM 當評分器前，必須意識到「同輸入重複打分會變」這個可量化的可靠性風險；重要評分不能只憑單次結果，可用重複評分 + 一致性指標（Kappa）檢查穩定度。
- 與我專案關係：weekly-reading 自己的五軸評分本身就是 LLM judge，這個風險直接適用——尤其兩篇總分接近時（如本週 23 vs 22）。
- evergreen，不寫死論文實驗細節。

## 3. Project-link（連 weekly-reading-ingest 本身）

- 為什麼相關：本工具的五軸評分是 LLM judge，可能 self-inconsistent；borderline 候選（總分差 1–2）的排序不該被當成精確。
- 可能應用：對 borderline 候選重跑一次評分看是否穩定，再決定主選。
- 不應直接套用：論文是大規模實驗 + 正式 Kappa 計算；單人週流程不需要正式統計，只取「單次評分不可盡信」的警示即可。

## 4. Review card（2 題）

- Q1：若 LLM 評分有 self-inconsistency，本週「主選 23 vs 備選 22」這 1 分差距可靠嗎？borderline 時該怎麼處理？（檢查判斷 / 連結既有知識）
- Q2：論文用 Kappa 量測重複一致性——這方法引入單人週流程是值得，還是過重？該用什麼輕量替代？（檢查判斷 / 應用）

## 5. Weekly log 更新

- 在 W26 段落增列「本週第二篇」：Rating Roulette，selected: backup A（額外加收），scores，note paths，caveats，status: ingested。
- 標明本週為使用者明確同意的「兩篇週」。

## Safety check 結果

- Free Access: Yes ✓｜domain: ai-engineering ✓｜source folder: papers ✓
- 不觸發 DOMAIN_DECISION / FREE_ACCESS_CHECK
- 不碰 meta/index.md（kb:index 重建）、meta/log.md、tools/kb、wiki/projects
- commit 前 git status 把關，只 add 本輪檔案
