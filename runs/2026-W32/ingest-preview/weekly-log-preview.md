> **PREVIEW** — 預計以「追加」方式寫入 `meta/weekly-reading/log.md` 檔尾（現有 W26 / W29 / W31 三節不動）
> 同時更新 frontmatter `updated: 2026-07-31` → `2026-08-09`。
> 尚未寫入 vault。

---

## 2026-W32

- Main pick: Adoption and Impact of Command-Line AI Coding Agents: A Study of Microsoft's Early 2026 Rollout of Claude Code and GitHub Copilot CLI — Emerson Murphy-Hill, Jenna Butler, Alexandra Savelieva — https://arxiv.org/abs/2607.01418
- Backup A: AI IDEs or Autonomous Agents? Measuring the Impact of Coding Agents on Software Development — Shyam Agarwal, Hao He, Bogdan Vasilescu（CMU）— https://arxiv.org/abs/2601.13597
  - Scores: Source Quality 4/5 / Idea Density 4/5 / Long-term Value 4/5 / Relevance 4/5 / Obsidian Fit 4/5（總分 20）
  - 未被選中；與 Main Pick 總分並列 20，但篇幅只有一半（10–12 頁對 23 頁），單位是開源倉庫而非個人開發者，離使用者實際情境較遠。**已作為 concept note 的對照材料實讀方法、結果與限制章節並引用完整 DiD 係數表，未建立獨立 source note**
- Backup B: Algorithmic management in the global gig economy: an interdisciplinary systematic literature review and critical discourse analysis — Bianca Ifeoma Chigbu — https://www.frontiersin.org/journals/sociology/articles/10.3389/fsoc.2026.1743445/full
  - Scores: Source Quality 4/5 / Idea Density 3/5 / Long-term Value 4/5 / Relevance 2/5 / Obsidian Fit 3/5（總分 16）
  - 未被選中；唯一經同行評審的候選，但為二手系統性綜述，且 Relevance 僅 2（與當前專案、工作流、學習路徑皆無接點）。`sociology` domain 至今仍為 0 篇 concept
- Selected: main
- Scores（main）: Source Quality 3/5 / Idea Density 5/5 / Long-term Value 3/5 / Relevance 5/5 / Obsidian Fit 4/5（總分 20）
- 選擇理由：不以總分決定（與 Backup A 並列 20）。唯一一篇研究對象等於使用者日常工具、樣本單位為個人開發者、且涵蓋「IDE Copilot 使用者轉向 CLI 代理」這條實際路徑的研究。Source Quality 僅 3 是刻意壓低：未經同行評審 + 作者三人皆 Microsoft 員工 + 研究對象含自家產品，方法嚴謹度雖高（含安慰劑檢定）但利益關係明確
- Domain 裁決：**ai-workflow**（`allowedConceptDomains` 內，無疑義，未觸發 DOMAIN_DECISION）。該 domain 先前僅 1 篇 concept，為活躍 domain 中最空者
- Note paths：
  - source: [[raw/sources/papers/2026-W32-cli-coding-agents-microsoft-rollout]]
  - concept: [[wiki/concepts/ai-workflow/coding-agent-productivity-proxy-gap]]
  - project-link: **本週未產**（五個專案中四個維護／完結、personal-website 未初始化，無一以 AI 工作流為對象，依規定不硬連）
  - review-card: **未產**（2026-08-01 起停產）
- User confirmed：yes（確認主選）
- 全文取得狀態：**已讀全文**（arXiv HTML v1 直接取得，無 redirect 或封鎖問題）。PDF 版本曾下載但本機 `pdftoppm` 未安裝無法解析，改走 HTML 入口，與 W31 情況相同
- Depth check（本輪實測）：concept **7,208 字** / source **4,522 字**；concept ≥ source ✅；≥ 6,000 ✅；章節覆蓋 8/8 ✅；全篇 `——` 0 處、粗體 3 處（符合每節至多 2 處）
- 補入的原始文獻：Agarwal et al. arXiv:2601.13597v2（Backup A，已實讀方法／結果／限制章節）。主選自身 23 頁厚度已足夠，此篇屬對照加值而非湊字數
- Caveats：
  - **arXiv 預印本，未經同行評審**，source/concept confidence 標 `medium`
  - **利益關係**：三位作者皆 Microsoft 員工，Microsoft 擁有 GitHub 並銷售 AI 工具。RQ4 結論為自家 Copilot CLI 提升達 Claude Code 的 2.2 倍（+24.9% vs +11.4%），作者自陳方向與公眾觀感相反、列兩個假說但均未檢驗，位置性聲明承認鄰近性可能形塑研究但無緩解措施。該數字不得單獨摘出引用
  - 產出指標單一：全篇僅量「28 天內合併的 PR 數」，作者自陳未測品質、可能增加複雜性、可能偏好小而頻繁的 PR
  - CausalImpact 處理組為自選採用者；安慰劑檢定（2025-10-06，−1.1% CI 跨零）只排除時序假象，未排除選擇偏誤
  - 劑量反應（+15.0% → +50.1%）作者明示為關聯非因果，高使用週可能含較輕任務組合
  - 外部效度窄：單一公司、16 週、2026 年初工具世代。作者自陳無法檢測長期衰減。RQ1 社會擴散結論（跳級同儕 25%+ → +216%）對個人開發者不適用
  - 論文初稿與第 4、5 節全部分析程式碼由 GitHub Copilot（Claude Opus 4.6–4.8）產出，作者已披露
  - 未回溯：He et al. 的 Cursor 合成控制研究僅透過本篇 Related Work 轉述得知，未取得原始文獻；RQ1／RQ2 完整迴歸係數表以圖表呈現，本次僅取得文字敘述中的點估計；論文總樣本數（工程師人數）在可取得內容中未列出。以上已在 concept note「未確認 / 待查證」逐項標注
- 本週選題同質性：主選與 Backup A 同屬 `ai-workflow`（刻意配對，兩者互為對照），Backup B 為 `sociology`。已在候選報告中聲明
- 本輪無規格變更
- Status：ingested（已正式寫入 vault）
