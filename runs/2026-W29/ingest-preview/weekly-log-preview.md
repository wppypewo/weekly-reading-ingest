# PREVIEW — weekly log

擬追加到：`meta/weekly-reading/log.md`（追加一節，不改既有內容；frontmatter 的 `updated` 改為 2026-07-18）

---

```markdown
## 2026-W29

- Main pick: Measuring Harness-Induced Belief Divergence in Multi-Step LLM Agents — Haiwen Yi, Xinyuan Song — https://arxiv.org/abs/2607.04528
- Backup A: Agent Skill Evaluation and Evolution: Frameworks and Benchmarks — Kexin Ding 等 6 人（含 Metaxas） — https://arxiv.org/abs/2606.11435
  - Scores: Source Quality 4/5, Idea Density 3/5, Long-term Value 4/5, Relevance 4/5, Obsidian Fit 4/5（總分 19）
  - 未被選中；survey 性質，給的是領域地圖而非機制。本週缺口是「執行環境如何改變結果」，不是「有哪些評估方法」
- Backup B: SkillGenBench: Benchmarking Skill Generation Pipelines for LLM Agents — Yifan Zhou 等 11 人 — https://arxiv.org/abs/2605.18693
  - Scores: Source Quality 3/5, Idea Density 4/5, Long-term Value 3/5, Relevance 3/5, Obsidian Fit 3/5（總分 16）
  - 未被選中；談自動生成 skill 的品質，而使用者的 skill 是手寫的，關聯較間接
- Selected: main
- Scores（main）: Source Quality 3/5 / Idea Density 5/5 / Long-term Value 4/5 / Relevance 5/5 / Obsidian Fit 5/5（總分 22）
- 選擇理由：不只看總分。唯一一篇把「執行環境本身」當變數量化的研究，直接對應 2026-07-18 完結的 skill-portability 實驗核心假說；並補上 vault 評估效度圖像的後半塊（既有 llm-judge-self-inconsistency 只涵蓋「評分者不穩定」）。Source Quality 僅 3 但仍選為主選——已符合軟門檻（SQ ≥ 3、Relevance ≥ 3、Free Access Yes、domain 合法）。
- Note paths：
  - source: [[raw/sources/papers/2026-W29-harness-induced-belief-divergence]]
  - concept: [[wiki/concepts/ai-engineering/harness-induced-belief-divergence]]
  - project-link: [[wiki/outputs/weekly-reading/project-links/2026-W29-harness-induced-belief-divergence]]
  - review-card: [[wiki/outputs/weekly-reading/review-cards/2026-W29-harness-induced-belief-divergence]]
- Review questions count：2
- User confirmed：yes（確認主選）
- 全文取得狀態：**已讀全文**（arXiv HTML 版；PDF 版 WebFetch 只回傳 binary，依 FAILURE-HANDLING 改走官方 HTML 入口重試成功）
- Caveats：preprint 未經同行評審；結果依賴作者自定的八欄位 belief schema；只建立相關未建立因果；受控實驗規模刻意小；與 skill-portability 實驗屬概念呼應而非同一件事，不得寫成「驗證了我的結論」；source/concept confidence 標 medium
- 本週選題同質性：三篇候選皆屬 ai-engineering 且主題相近。design domain 在 vault 為 0 篇且 fashion-archive 剛完工，本應是明顯缺口，但本輪只搜到 SEO 內容農場等級的「2026 設計趨勢」列表文，不符品質門檻，依規定不硬湊
- Status：ingested（已正式寫入 vault）
```
