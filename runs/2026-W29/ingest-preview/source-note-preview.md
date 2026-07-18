# PREVIEW — source note

擬寫入路徑：`raw/sources/papers/2026-W29-harness-induced-belief-divergence.md`

---

```markdown
---
type: source
status: raw
domain: ai-engineering
source: arXiv
author: Haiwen Yi, Xinyuan Song
published: 2026-07（arXiv 2607.04528）
created: 2026-07-18
processed: true
confidence: medium
related_concepts: ["[[wiki/concepts/ai-engineering/harness-induced-belief-divergence]]"]
tags: [weekly-reading]
---

# Measuring Harness-Induced Belief Divergence in Multi-Step LLM Agents

## Source

- Title: Measuring Harness-Induced Belief Divergence in Multi-Step LLM Agents
- Author: Haiwen Yi, Xinyuan Song
- URL: https://arxiv.org/abs/2607.04528
- Code: https://github.com/Hik289/Harness-induce-bias.git
- Language: English
- Source Type: arXiv preprint（未見同行評審紀錄）
- Free Access: Yes（PDF / HTML / TeX 皆開放）
- Estimated Reading Time: 28 頁，約 90–120 分鐘

## 原始摘錄 / 摘要

### Selected Short Excerpts（節錄，僅作引用線索）

> harness design 是實驗變數，而非單純的實作細節。

### 摘要（繁體中文重寫，非逐句翻譯）

評估用的 harness——負責中介 agent 的觀察、動作與修復的那層系統——會改變 agent 的內部信念，即使模型與任務都固定不變。作者提出 belief-rollout 診斷法，檢視 K 步軌跡在進度、風險等維度上的表現，並把跨 harness 的信念分歧拆解成兩個成分：即時的介面位移（arrival）與隨步數累積的變化（growth）。在編碼任務上，阻擋動作或選擇性驗證這類設計選擇會在維持成功率的同時改變底層信念。作者另提出 BIWM 協議，用來正規化觀察並對齊不同 harness 配置下的信念軌跡。

## 我自己的註記

### 我的閱讀理由

skill-portability 實驗（2026-07-18 完結）的核心假說是「內容層可移植，執行層綁定 Claude harness 訓練」。這篇把「執行環境」本身當成可量化的實驗變數，是該假說在文獻上的對口研究。

### 實驗設定（已讀全文）

- 固定基礎 LLM；三個 benchmark 家族：HIBench-Code（8 個受控編碼任務）、SWE-bench Verified、Terminal-Bench；受控研究使用相同隨機種子。
- 六種 harness：H₀ 原始參照 / H₁ 結構化 / H₂ 風險閘門 / H₃ 重修復 / H₄ 選擇性驗證 / H₅ 成本感知。

### 關鍵數據

- HIBench-Code，K=5：整體 belief divergence 0.402–0.479；arrival 逼近 1.0，growth 僅 0.147–0.257。
- K=5 → K=20 整體分歧無系統性上升；但數值預測持續變動（K=1 的 0.044 → K=16 的 0.136）。
- SWE-bench Verified：風險閘門下失敗歸因分歧由 K=3 的 0.400 升至 K=5 的 0.800。
- BIWM 全套 instrumentation 使 growth divergence 增加 0.087–0.226；repair-unrolled logging 單項影響最大（重修復 harness +0.195）。

### 候選評分（來自本週候選報告）

- Source Quality: 3/5 — arXiv preprint，兩位作者，無明確機構背書，未見同行評審
- Idea Density: 5/5 — 六種 harness × 三個 benchmark，belief 分解與 BIWM 協議，表格數據具體
- Long-term Value: 4/5 — 框架有持久價值，具體指標可能被取代
- Relevance: 5/5 — 直接對應 skill-portability 的核心假說
- Obsidian Fit: 5/5 — 可與既有 llm-judge-self-inconsistency 組成評估效度概念群

### Caveats

- **preprint，未經同行評審**。
- 結果依賴作者自定的**八欄位 belief schema**（作者自陳），換一套表徵可能得到不同的成分拆解。
- **只能建立相關、無法建立因果**（作者自陳）：belief 分歧與後續行動改變是相關關係。
- 受控實驗規模刻意小（作者優先機制歸因而非覆蓋率）；公開 benchmark 數值不應解讀為整體效能估計。
- **與 skill-portability 實驗是概念層呼應，不是同一件事**：該實驗測 skill 內容跨平台移植的效益衰減，本文測 harness 中介如何改變 agent 內部信念。不得寫成「本文驗證了我的實驗結論」。

## 待處理問題

- 八欄位 belief schema 的具體欄位定義為何？若換成其他表徵，arrival / growth 的拆解是否仍成立？
- BIWM 的對齊代價（instrumentation 反而增加 growth divergence）在實務上如何取捨？

## 處理紀錄

- 2026-07-18：2026-W29 主選，正式 ingest。全文以 arXiv HTML 版讀取（PDF 版 WebFetch 只回傳 binary）。
- 2026-07-18：依 processedPolicy 標 `processed: true`（同輪已產出 concept [[wiki/concepts/ai-engineering/harness-induced-belief-divergence]]）。
```
