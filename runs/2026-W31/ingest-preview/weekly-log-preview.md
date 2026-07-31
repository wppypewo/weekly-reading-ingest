> **PREVIEW** — 預定**追加**至 `meta/weekly-reading/log.md` 檔尾（不改動既有內容）
> 尚未寫入 vault。

---

```markdown
## 2026-W31

- Main pick: Machine learning uncovers the most robust self-report predictors of relationship quality across 43 longitudinal couples studies — Samantha Joel, Paul W. Eastwick 等 86 位研究者 — https://www.pnas.org/doi/10.1073/pnas.1917036117（免費全文 https://pmc.ncbi.nlm.nih.gov/articles/PMC7431040/）
- Backup A: What Is Social Connection in the Context of Human Need: An Interdisciplinary Literature Review — Kyla L. Bauer, Rachel Johnson-Koenke, Meredith P. Fort — https://pmc.ncbi.nlm.nih.gov/articles/PMC11941835/
  - Scores: Source Quality 2/5, Idea Density 4/5, Long-term Value 3/5, Relevance 3/5, Obsidian Fit 3/5（總分 15）
  - 未被選中；厚度足夠（12,000–14,000 字）但為 purposive 選取 44 篇的非系統性回顧，發表於 MDPI，且停在定義層不給機制
- Backup B: How studying friendship has changed the way I understand my own loneliness — Marie-Elisabeth Lei Pihl — https://theconversation.com/how-studying-friendship-has-changed-the-way-i-understand-my-own-loneliness-281767
  - Scores: Source Quality 3/5, Idea Density 3/5, Long-term Value 4/5, Relevance 4/5, Obsidian Fit 4/5（總分 18）
  - 未被選中；原為 v2 主選，因 3,500 字撐不起新的 8,000 字 concept note 下限而降級。且其引用的兩項關鍵數據（「超過 40% 成年人希望有更親近友誼」、「每週不到 3 小時 vs 十年前 6 小時」）原文未給出處、無法定位，回溯清單不完整，依新規格喪失主選資格
- Selected: main
- Scores（main）: Source Quality 5/5 / Idea Density 5/5 / Long-term Value 5/5 / Relevance 4/5 / Obsidian Fit 5/5（總分 24）
- 選擇理由：本工作流至今出現過的最高等級來源（PNAS，43 個縱貫資料集、29 個實驗室、86 位研究者整合）。它給的不是又一個相關性，而是一條邊界——自陳測量在親密關係上能做到什麼、做不到什麼。同時是 vault 六個 concept domain 至今第一篇處理人際關係的筆記，並能與既有兩篇評估效度筆記接成第一條跨 domain 概念線。
- Note paths：
  - source: [[raw/sources/papers/2026-W31-relationship-quality-predictability]]
  - concept: [[wiki/concepts/psychology/relationship-quality-predictability-limits]]
  - project-link: **本週未產**（五個專案皆為技術性專案，無實質關聯，依規定不硬連）
  - review-card: [[wiki/outputs/weekly-reading/review-cards/2026-W31-relationship-quality-predictability]]
- Review questions count：2
- User confirmed：yes（確認主選）
- 全文取得狀態：**已讀全文**（PMC7431040 免費全文；PNAS 官網回 403，依 FAILURE-HANDLING 改走 PMC 入口重試成功）
- 本輪規格變更：本週為 concept note 深度規格訂立後的第一輪 ingest。新增 `allowedConceptDomains`：`psychology`、`sociology`；`vaultRoot` 由 Windows 路徑改為 Mac 路徑；`templates/concept-note.md` 新增 `## 我的辨證` 章節；curate 新增 Source Weight 與深度可行性欄位；ingest 新增深度規格與 `DEPTH_CHECK` 狀態
- Caveats：2020 年論文，非近期內容，後續五年複驗狀況尚未查證；全部資料集取自西方國家（美、加、瑞士、紐西蘭、荷蘭、以色列），跨文化外推未經檢驗；**2,413 項測量中 99.4% 為自陳量表**，因此「變化不可預測」無法區分是變化本身難測還是自陳測不到，不得寫成前者；心理學實驗室資料集比例高於社會學／傳播／家庭研究，作者自陳學科偏誤；「自己的感受解釋一切」為中介關係，不得寫成「伴侶不重要」；source/concept confidence 標 high（同行評審 + 整合分析），但上述限制須在 concept note 中明列
- 本週選題同質性：主選屬 psychology、兩篇備選屬 sociology，已脫離 W29 起連續兩輪 ai-workflow 單一 domain 的狀態
- 外刊管道首次啟用：Aeon 連續三次回 HTTP 429，三篇原鎖定 essay 無法取得全文，依規定不以摘要評分，本輪未列入。付費牆刊物依 `freeOnly: true` 未納入搜尋
- Status：ingested（已正式寫入 vault）
```

---

## ⚠️ 另需你裁示（不在本次追加範圍內）

`meta/weekly-reading/log.md` 第 11 行的說明文字仍寫著 Windows 路徑：

```
候選報告暫存於工具專案 `D:\ClaudeCode\projects\weekly-reading-ingest\runs\`，未確認不進此檔。
```

Mac 上該路徑不存在，正確應為 `~/ClaudeCode/projects/weekly-reading-ingest/runs/`。

**我不會順手改**——你這次批准的是追加 W31 條目與更新 `wiki/concepts/README.md`，不含這行。要一起改請明說。
