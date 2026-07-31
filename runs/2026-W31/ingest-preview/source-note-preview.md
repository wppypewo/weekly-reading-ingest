> **PREVIEW** — 預定寫入 `raw/sources/papers/2026-W31-relationship-quality-predictability.md`
> 尚未寫入 vault。

---

```markdown
---
type: source
status: raw
domain: psychology
source: PNAS
author: Samantha Joel, Paul W. Eastwick, et al.（共 86 位研究者）
published: 2020-08-11（PNAS 117(32): 19061–19071，DOI 10.1073/pnas.1917036117）
created: 2026-07-31
processed: true
confidence: high
related_concepts: ["[[wiki/concepts/psychology/relationship-quality-predictability-limits]]"]
tags: [weekly-reading]
---

# Machine Learning Uncovers the Most Robust Self-Report Predictors of Relationship Quality Across 43 Longitudinal Couples Studies

## Source

- Title: Machine learning uncovers the most robust self-report predictors of relationship quality across 43 longitudinal couples studies
- Author: Samantha Joel、Paul W. Eastwick 等，共 86 位關係科學研究者、29 個實驗室
- URL: https://www.pnas.org/doi/10.1073/pnas.1917036117
- 免費全文: https://pmc.ncbi.nlm.nih.gov/articles/PMC7431040/（PMC7431040）
- Language: English
- Source Type: 同行評審期刊論文（PNAS）
- Free Access: Yes（PMC 免費全文）
- Source Weight: 11 頁（19061–19071）＋ Supplementary Information
- Estimated Reading Time: 約 120–150 分鐘（統計密集）
- 資助: 39 筆國家級／大學級補助

## 原始摘錄 / 摘要

### Selected Short Excerpts（節錄，僅作引用線索）

> "Individual differences and partner reports had no predictive effects beyond
> actor-reported relationship-specific variables alone."

> "Change in relationship quality was largely unpredictable from any combination
> of self-report variables."

> "Any nascent signal of whether a relationship is going to become better or worse
> over time does not seem to be detectable in self-reported variables at baseline."

### 繁中重寫摘要

這是一項整合 43 個縱貫伴侶資料集的大規模分析，目的有二：量化關係品質到底有多可預測，以及找出哪些變數能穩定預測它。

資料規模：基線 22,163 人、11,196 對伴侶、43 個縱貫資料集、來自 29 個實驗室、86 位研究者、39 筆研究資助。追蹤平均 4 個時間點、橫跨 14 個月（範圍為 2–11 個時間點、2–48 個月）。基線共收集 2,413 項自陳測量，其中 1,149 項為關係特定變數。

方法採 Random Forests：每個模型 5,000 棵回歸樹，`mtry` 使用預設值（預測變數總數的三分之一），以 VSURF 套件做變數篩選，樣本外表現以 out-of-bag 樣本估計。每個資料集跑 21 個模型，分別預測基線滿意度、追蹤滿意度、滿意度變化；含承諾變數的資料集另跑 21 個。

主要發現有四層。第一，關係特定變數的預測力明顯高於個人差異變數。第二，自己報告的變數比伴侶報告的變數強上二到四倍。第三，也是最關鍵的：把所有變數合併之後，解釋力並未超過「只用自己報告的關係特定變數」。第四，關係品質的「變化」幾乎無法從基線自陳資料預測，所有分析都解釋不到 5% 的變異。

作者據此對未來的關係理論提出四項約束，並提出一個中介式解釋：個人差異與伴侶效應確實重要，但它們是透過人際歷程間接發揮影響，而那些歷程已被自己報告的關係變數充分捕捉。

## 關鍵數據

### 預測力排序（成功率）

關係特定變數：感知伴侶承諾 85%／親密感 81%／感激 72%／愛 71%／性滿意度 71%／感知伴侶滿意度 70%／衝突 69%／感知伴侶回應性 69%／信任 68%／投入 67%

個人差異變數：生活滿意度 88%／憂鬱 74%／負向情感 73%／焦慮型依戀 71%／逃避型依戀 70%／年齡 68%／焦慮 66%／自尊 58%／親和性 54%／正向情感 54%

### 變異量解釋

| 變數組合 | 基線滿意度 | 追蹤滿意度 |
|---|---|---|
| 自己報告的關係變數 | 45% | 18% |
| 自己報告的個人變數 | 19% | 12% |
| 伴侶報告的關係變數 | 15% | 7% |
| 伴侶報告的個人變數 | 5% | 5% |
| 自己＋伴侶報告的關係變數 | 46% | — |
| 全部合併 | 44% | — |

滿意度「變化」：所有分析皆低於 5%，且所有估計的信賴區間大幅重疊。

## 作者自陳限制

1. 所有資料集皆取自西方國家（美國、加拿大、瑞士、紐西蘭、荷蘭、以色列），跨文化外推未經檢驗。
2. 2,413 項測量中 **99.4% 為明確的自陳評分量表**，而非直接捕捉實時行為的獨立觀察。作者建議未來納入觀察資料與情境變數，並具體點名報稅資料、日間皮質醇節律、他人評定。
3. 資料集中來自心理學實驗室者，比例高於社會學、傳播學、家庭研究；不同學科常用的變數可能導出不同結論。
4. 樣本同質性疑慮仍在，雖已納入刻意過採低收入族群的 Supporting Healthy Marriages Project。
5. 作者明言關係品質的變化不可預測，「很可能是因為變化取決於外部情境、行為歷程，或其他本身也在變動的因素」。

## 待查證

- 2020 年至今（2026-07）的後續複驗、反駁或延伸研究狀況，尚未查。
- Supplementary Information 未逐項讀完。
```
