# PREVIEW — concept note

擬寫入路徑：`wiki/concepts/ai-engineering/harness-induced-belief-divergence.md`

---

```markdown
---
type: concept
status: evergreen
maturity: seed
evidence_level: mixed
confidence: medium
source_count: 1
domain: ai-engineering
source_notes: ["[[raw/sources/papers/2026-W29-harness-induced-belief-divergence]]"]
created: 2026-07-18
updated: 2026-07-18
tags: [weekly-reading]
---

# 評估 harness 作為實驗變數

## 核心結論

跑 agent 的那層系統——負責決定 agent 看得到什麼觀察、能執行哪些動作、失敗後怎麼修復——**不是中立的管道**。即使模型與任務完全固定，只要換一種 harness 中介方式，agent 的內部信念就會顯著分歧。因此「這個 agent 有多強」這種說法，若不連同 harness 設定一起報告，本身就是不完整的。

## 背後原因

harness 決定了 agent 賴以推理的資訊長什麼樣子。把原始堆疊追蹤解析成結構化狀態、在執行前阻擋高風險動作、自動重試並套用修補——這些設計都在改寫 agent 所處的觀察空間。成功率可能不變，但通往結果的信念路徑已經不同。

## 一個值得記住的拆解

論文把跨 harness 的信念分歧拆成兩個成分：

- **arrival（即時介面位移）**：換 harness 的當下就產生的差異。實測逼近 1.0。
- **growth（隨步數累積）**：長程演化出來的差異。實測僅 0.147–0.257。

**多數分歧來自介面本身，不是長程累積。** 另一個反直覺的觀察：整體分歧在 K=5 到 K=20 之間不再系統性上升，但數值型預測仍持續飄移（0.044 → 0.136）——**整體看似穩定，不代表每個面向都穩定**。

## 使用場景

- 比較兩個 agent 的效能數字時，先確認它們跑在相同 harness 上；否則差異可能來自環境而非能力。
- 設計評估流程時，把 harness 設定當成必須記錄的實驗參數，而不是實作細節。
- 觀察到 agent 行為改變時，先排除「是不是我改了執行環境」再歸因到模型或提示。

## 與我目前專案 / 學習的關係

與 [[wiki/projects/skill-portability/current-status|skill-portability 實驗]]同屬一個問題意識。該實驗的假說是「內容層可移植、執行層綁定 Claude harness」，本文則證明 harness 中介方式本身就足以造成信念分歧。

**但兩者測的不是同一件事**：該實驗測的是 skill 內容跨平台移植後的效益衰減（以人工盲評打分），本文測的是同一模型在不同 harness 下的內部信念分歧（以 belief-rollout 診斷）。本文**不構成**對該實驗結論的驗證，只是提供一個可對照的機制視角——尤其是「分歧主要來自即時介面而非長程累積」這點，與該實驗觀察到的「執行層未崩塌、只呈邊緣侵蝕」值得並置思考。

## 與既有概念的互補

[[wiki/concepts/ai-engineering/llm-judge-self-inconsistency]] 講的是**評分者不穩定**，本篇講的是**執行環境不中立**。兩者合起來才構成完整的評估效度圖像：分數會飄，跑分數的環境也會改變被測對象。

## 來源

- [[raw/sources/papers/2026-W29-harness-induced-belief-divergence]]

## 未確認 / 待查證

- 論文結果依賴作者自定的八欄位 belief schema；換一套表徵是否仍得到相同的 arrival / growth 拆解，未知。
- 論文只建立相關、未建立因果（作者自陳）：belief 分歧是否直接導致下游行動改變，尚未證實。
- preprint，未經同行評審。

## 相關概念

- [[wiki/concepts/ai-engineering/llm-judge-self-inconsistency]]（評估效度的另一面）
- [[wiki/concepts/ai-workflow/agents-md-design-checklist]]（同屬「如何讓 AI 工作流更可靠」的判準）
```
