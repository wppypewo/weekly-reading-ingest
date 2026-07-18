# Weekly Reading Candidates｜2026-W26（第二次 curate，AI 主題）

> ⚠️ 本週（2026-W26）已 ingest 過一篇（首篇 commit `e0161bb`，記於 `meta/weekly-reading/log.md`）。本次為同週第二次 curate。curate 階段不寫 vault；若你之後要 ingest 本報告的主選，會違反「每週一篇」原則並使 W26 log 出現兩筆——屆時請明確決定。
>
> 三篇候選皆真實搜尋並以 WebFetch 驗證內容、長度與 Free Access。

## 本週主題判斷

- 預設主題：AI（使用者指定）。在 AI 範圍內收斂到「LLM 系統的 context 管理與評分可靠性」，刻意避開首篇已覆蓋的「coding agent workflow / AGENTS.md 設計」。
- 選題理由：本工具自身的已知缺口（audit 4.5 指出 weekly-reading 評分偏主觀、缺校準），與「context 管理」「LLM 評分偏誤」兩個子題直接相關。
- 是否使用使用者手動連結：否，全部自動搜尋。
- 是否含當週熱門內容：否，三篇皆以品質門檻篩出，非排行榜。

---

## Main Pick

- Title: Effective context engineering for AI agents
- Author: Anthropic Applied AI 團隊（Prithvi Rajasekaran、Ethan Dixon、Carly Ryan、Jeremy Hadfield 等，具名）
- Source: Anthropic 官方工程部落格
- URL: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Language: English
- Estimated Reading Time: 約 12–15 分鐘
- Type: 公司工程 essay
- Free Access: Yes
- Topic: context engineering / agent 設計原理

### Scores

- Source Quality: 5/5 — Anthropic 官方工程團隊、作者具名、一手實作經驗，非轉述
- Idea Density: 5/5 — 系統提示「適當高度」框架、工具設計三原則、長任務三層方案（compaction / note-taking / sub-agent），含可直接套用對照表
- Long-term Value: 4/5 — context engineering 屬基礎原理可長期沿用，但部分 token 數字與技術細節會隨模型演進
- Relevance: 4/5 — 與 agent/LLM 工作流設計相關；對「weekly-reading 評分缺口」不如 Backup A 直接，但與首篇形成「workflow + context」互補
- Obsidian Fit: 5/5 — 可拆成乾淨可複用概念（context 預算、compaction、結構化筆記記憶），domain `ai-engineering` 已有先例

**Domain 預判**：`ai-engineering`（vault 已有 `wiki/concepts/ai-engineering/claude-code-memory-skills-hooks-context-management`，主題契合）

---

## Backup A

- Title: Rating Roulette: Self-Inconsistency in LLM-As-A-Judge Frameworks
- Author: Haldar & Hockenmaier（arXiv preprint，CC BY 4.0）
- Source: arXiv
- URL: https://arxiv.org/pdf/2510.27106
- Language: English
- Type: Paper
- Free Access: Yes
- Recommendation reason: 直接打中本工具評分機制的核心缺口——「用 LLM 做評分會自我不一致」。對改進 weekly-reading 的五軸 rubric 最對口，但屬學術論文需轉譯、且偏診斷少緩解。

### Scores

- Source Quality: 5/5 — 學術論文，CC BY 4.0，跨多模型（Claude / DeepSeek-R1 / Qwen）系統實驗
- Idea Density: 4/5 — 用 Cohen's / Fleiss' Kappa 量化評判一致性，扎實；但緩解建議較少
- Long-term Value: 5/5 — 方法論與量測框架不易過時
- Relevance: 5/5 — 與「我設計的評分 rubric 是否可靠」直接相關，補的是 audit 已點名的主觀性缺口
- Obsidian Fit: 3/5 — 19 頁論文，需較多轉譯才能變成可複用 concept

**Domain 預判**：`ai-engineering`

---

## Backup B

- Title: LLM-as-a-Judge vs Human Evaluation
- Author: Pratik Bhavsar（Galileo Labs）
- Source: Galileo Labs 部落格
- URL: https://galileo.ai/blog/llm-as-a-judge-vs-human-evaluation
- Language: English
- Type: Article（公司部落格）
- Free Access: Yes
- Recommendation reason: 整理 self-preference / position / verbosity 等評分偏誤並給混合評估框架，可讀性高；但含自家產品（promptquality/ChainPoll）範例，商業成分需剝離，長期價值打折。

### Scores

- Source Quality: 4/5 — 公司部落格、作者具名、引用同行評審研究，但夾帶自家工具推廣
- Idea Density: 4/5 — 偏誤清單 + 何時用人類 vs LLM 的決策框架 + 代碼範例
- Long-term Value: 3/5 — 含自家 product API 範例，會隨產品變動過時
- Relevance: 4/5 — 評分偏誤與本工具評分相關，但實務性高於原理性
- Obsidian Fit: 3/5 — 需剝離商業成分才能沉澱

**Domain 預判**：`ai-engineering`

---

## 五項評分總表

| | Source Quality | Idea Density | Long-term Value | Relevance | Obsidian Fit | 總分 |
|---|---|---|---|---|---|---|
| Main Pick（Anthropic） | 5 | 5 | 4 | 4 | 5 | 23 |
| Backup A（Rating Roulette） | 5 | 4 | 5 | 5 | 3 | 22 |
| Backup B（Galileo） | 4 | 4 | 3 | 4 | 3 | 18 |

## Main Pick 勝出理由（不只看總分）

- **為何是主選**：三篇中可信度與可沉澱性都最高（Source Quality 5 + Obsidian Fit 5）。Anthropic 官方一手研究，作者具名，框架可直接拆成乾淨 concept；與首篇（workflow 選擇）互補，補的是「agent 的 context 預算如何分配與壓縮」這個首篇沒深入的缺口。
- **為何勝過 Backup A**：Backup A（Rating Roulette）Relevance 更高、總分僅低 1 分，但它是同行評審前的 preprint、19 頁需大量轉譯（Obsidian Fit 3），且偏「診斷問題」少「可操作解法」。從「本週能不能直接讀完並沉澱」角度，Main Pick 成本更低、可複用度更高。
- **為何勝過 Backup B**：Backup B 夾帶自家產品推廣，長期價值打折（3），純度不如 Anthropic 的中立工程論述。
- **滿足軟門檻**：Source Quality 5≥3、Relevance 4≥3、Free Access Yes、domain `ai-engineering` ∈ allowed。✅

## 風險與限制

- 三篇皆單次 WebFetch 驗證，未交叉比對，concept note 若產生應標 `confidence: medium`。
- Main Pick 部分 token 數字（如 sub-agent 回傳 1000–2000 token）屬當下經驗值，concept 應只保留原則，不寫死數字。
- **同週第二篇問題**：本週 W26 已 ingest 一篇，若 ingest 本主選會出現同週兩筆，需你決定是否接受、或改記為下一週。

## 建議產生的 Concept Note（若選 Main Pick）

- `context-budget-and-compaction`（context 是有限資源：預算分配、compaction、結構化筆記記憶）— domain：`ai-engineering`
- （只建議 1 篇；工具設計三原則、系統提示「適當高度」可留 source note 的「後續可萃取概念」，不一次拆多篇）

## 可能的 Project Link

- **weekly-reading-ingest / Ricky-KnowledgeBase**：文中「context 是有限資源、找最小高訊號 token 集合」可反過來檢查我把 SKILL.md 拆成 SAFETY.md / FAILURE-HANDLING.md / MODES.md 的分層是否符合此原則。
- portfolio-tracker / movie-app / fashion-archive：本週沒有明確專案連結。

## Free Access 判斷依據

| 候選 | Free Access | 依據 |
|---|---|---|
| Main Pick | Yes | Anthropic 官方工程 blog，全文公開，無付費/註冊牆 |
| Backup A | Yes | arXiv 公開 preprint，CC BY 4.0 |
| Backup B | Yes | Galileo 公司 blog，全文公開，無註冊牆 |

三篇皆 Yes，預期不觸發 FREE_ACCESS_CHECK 攔截。

## 互動選項

1. 確認主選
2. 改選備選 A
3. 改選備選 B
4. 補連結後重評
5. 重新搜尋
6. 本週跳過
