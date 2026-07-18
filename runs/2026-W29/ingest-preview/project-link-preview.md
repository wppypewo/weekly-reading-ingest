# PREVIEW — project link

擬寫入路徑：`wiki/outputs/weekly-reading/project-links/2026-W29-harness-induced-belief-divergence.md`

---

```markdown
---
type: output
output_kind: project-link
curation_week: 2026-W29
related_source: "[[raw/sources/papers/2026-W29-harness-induced-belief-divergence]]"
related_project: skill-portability
domain: ai-engineering
related_domains: []
tags: [weekly-reading, project-link]
created: 2026-07-18
---

# Harness-Induced Belief Divergence — Project Link

## 關聯專案

[[wiki/projects/skill-portability/current-status|skill-portability]]（Skill 可移植性實驗）。

> 該專案已於 2026-07-18 完結，本連結屬**回溯性補充**，不是後續開發依據。

## 為什麼相關

該實驗的核心假說是「內容層（規則／詞彙／範例）可移植，執行層（逐步展開、自檢）綁定 Claude harness 訓練」。本文獨立地把「harness 中介方式」當成可量化的實驗變數，證明即使模型與任務固定，換一種 harness 就足以讓 agent 內部信念顯著分歧。

兩者共享同一個問題意識：**執行環境不是中立的**。

## 可能的應用方式

- 若日後改版報告，本文可作為「執行層綁定執行環境」這個論點的外部文獻依據，補上該實驗目前只有自家數據的弱點。
- 本文的 arrival / growth 拆解提供了一個現成的分析角度：該實驗觀察到的「邊緣侵蝕」（缺詩題、檢查表文字漂移、策略欄結構漂移）究竟屬於即時介面差異，還是長程累積效應？這是原報告未區分的維度。

## 不應該直接套用的地方

- **兩者測的不是同一件事**。該實驗測 skill 內容跨平台移植的效益衰減，用人工盲評打分；本文測同一模型在不同 harness 下的內部信念分歧，用 belief-rollout 診斷。**不得**把本文寫成「驗證了我的實驗結論」。
- 本文只建立相關、未建立因果（作者自陳），不能拿來主張「harness 造成了我實驗中的分數差異」。
- 本文是 preprint，未經同行評審；作為報告引用時須標明來源狀態。
- 本文的 belief schema 是作者自定的八欄位，不是通用標準，不宜直接搬到該實驗的評分架構上。
```
