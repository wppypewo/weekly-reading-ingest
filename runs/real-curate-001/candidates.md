# Weekly Reading Candidates｜REAL-CURATE-001

> 本次為 `weekly-reading-curate` 第一次真實搜尋測試。三篇候選皆為真實搜尋結果，已用 WebFetch 驗證內容、長度與 Free Access。**本報告只輸出於此與 Claude 回覆，未寫入 Obsidian vault，未呼叫 `weekly-reading-ingest`。**

## 本週主題判斷

- 預設主題：AI agent / Claude Code 協作工作流（方向 1）
- 選題理由：本週實際工作就是設計 `weekly-reading-curate` / `weekly-reading-ingest` 兩個 Claude Code skill，直接補的是「如何設計可靠的 agentic workflow / skill 文件 / context 管理」這個正在發生的知識缺口
- 是否使用使用者手動連結：否，全部為本次自動搜尋結果
- 是否有當週熱門內容：否，三篇皆非「熱門排行榜」類型，是以品質門檻篩出的 essay / 原始筆記 / 學術綜述

---

## Main Pick

- Title: A Survey of Development Workflows in the Coding Agent Era
- Author: 逆瀬川ちゃん（Sakasegawa-chan，@gyakuse）
- Source: 作者個人技術部落格
- URL: https://nyosegawa.com/en/posts/coding-agent-workflow-2026/
- Language: English
- Estimated Reading Time: 約 25 分鐘
- Type: Essay
- Free Access: Yes
- Topic: agentic coding workflow / Claude Code / AGENTS.md 設計

### Scores

- Source Quality: 4/5 — 作者原站發表，含具體案例與框架，但屬個人技術部落格，非同行評審
- Idea Density: 5/5 — 提供至少 5 個結構化決策框架（workflow 選擇矩陣、context engineering 失敗模式表、會話複雜度光譜、AGENTS.md 檢查清單、權限最小化清單），密度極高
- Long-term Value: 3/5 — 引用具體工具/repo（如 19 個智能體的 oh-my-claudecode），半年後部分細節可能過時，但決策框架本身可長期沿用
- Relevance: 5/5 — 直接對應本週實際在做的事（設計 weekly-reading-curate / weekly-reading-ingest 兩個 skill 文件）
- Obsidian Fit: 4/5 — 可拆成多個獨立 concept（workflow 選擇矩陣、AGENTS.md 設計檢查清單、context engineering 失敗模式），domain 落在既有 `ai-workflow` 沒有疑義

**Domain 預判**：`ai-workflow`（vault 已有 `wiki/concepts/ai-workflow/Claude-Code/` 子資料夾，直接契合，不需人工決策）

---

## Backup A

- Title: Evergreen notes
- Author: Andy Matuschak
- Source: 作者個人筆記網站（notes.andymatuschak.org）
- URL: https://notes.andymatuschak.org/Evergreen_notes
- Language: English
- Type: Essay（個人筆記形式）
- Free Access: Yes
- Recommendation reason: 是「evergreen note」這個方法論的原始源頭文章，本 vault 的 `templates/concept-note.md` 本身就採用 `status: evergreen` 設計，這篇是該設計背後的理論源頭，但與本週主軸（Claude Code agentic workflow）關聯較弱，且無法歸入既有五個 domain

### Scores

- Source Quality: 5/5 — 該領域最早系統化論述「evergreen notes」概念的原始來源，被後續大量 PKM 文章引用
- Idea Density: 4/5 — 短文但五項原則（原子性、概念導向、密集連結、關聯本體、為自己寫作）密度高，幾乎沒有贅字
- Long-term Value: 5/5 — 理論不受工具版本影響，至今仍是 PKM 領域標準參照
- Relevance: 3/5 — 與本週「Claude Code agentic workflow」主軸關聯較弱，但與「weekly-reading-ingest 自身的 concept note 設計」有間接關聯
- Obsidian Fit: 2/5 — **無法合理歸入既有五個 domain**（ai-engineering / ai-workflow / design / finance / french），依規則降低評分

**Domain 預判**：**無法歸入既有五個 domain** → 若被選為 ingest 對象，需標記「需要人工 domain 決策」，依規格**原則上不得列為 Main Pick**。

---

## Backup B

- Title: Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers
- Author: Pengfei Du（arXiv preprint，CC BY 4.0；Hong Kong Research Institute of Technology）
- Source: arXiv
- URL: https://arxiv.org/html/2603.07670v1
- Language: English
- Type: Paper
- Free Access: Yes
- Recommendation reason: 完全開放的學術綜述，提出記憶機制的三維分類法（時間範圍 / 表示基底 / 控制策略），長期價值高，但篇幅長、偏理論，與本週實際任務的直接相關性低於 Main Pick

### Scores

- Source Quality: 5/5 — 學術綜述，70+ 參考文獻，CC BY 4.0 完全開放
- Idea Density: 4/5 — 三維分類法與四層評估棧紮實，但部分內容為形式化定義，可直接套用的「決策」少於 Main Pick
- Long-term Value: 5/5 — 形式化框架不易因實作工具變動過時
- Relevance: 4/5 — 與 agent memory 設計相關，但比起本週 KB skill 實作的直接需求略偏理論
- Obsidian Fit: 3/5 — 內容紮實但篇幅長（10 章節 + 70 參考文獻），需要較多轉譯工夫才能拆成 concept

**Domain 預判**：`ai-engineering`（既有 domain，無疑義）

---

## 五項評分總表

| | Source Quality | Idea Density | Long-term Value | Relevance | Obsidian Fit | 總分 |
|---|---|---|---|---|---|---|
| Main Pick | 4 | 5 | 3 | 5 | 4 | 21 |
| Backup A | 5 | 4 | 5 | 3 | 2 | 19 |
| Backup B | 5 | 4 | 5 | 4 | 3 | 21 |

## Main Pick 勝出理由

**Main Pick 總分與 Backup B 並列最高（21），不是靠總分勝出，而是依規格要求的質化判斷：**

- **為什麼是本週主選**：本週實際工作就是設計 agentic skill 文件（`weekly-reading-curate` / `weekly-reading-ingest`），這篇文章提供的 5 個決策框架（尤其是 AGENTS.md 設計檢查清單、context engineering 失敗模式表）可直接拿來自我檢查現有兩份 SKILL.md 的設計品質。
- **為什麼比 Backup A 更適合**：Backup A 雖然 Source Quality / Long-term Value 更高，但與本週任務關聯弱，且明確卡在 domain 規則（無法歸入既有五個 domain），若強行選它會立刻進入 `DOMAIN_DECISION` 流程，不符合「本週該讀什麼」的效率考量。
- **為什麼比 Backup B 更適合**：Backup B 總分相同，但屬學術綜述，篇幅長、偏理論形式化，從「這週能不能直接拿來用」的角度，Relevance 與 Obsidian Fit 都略低於 Main Pick；Backup B 更適合「之後要做 agent memory 功能」時再讀，不是本週最急迫的缺口。
- **補的知識缺口**：「如何把鬆散的 workflow 直覺，轉成可檢查、可重用的決策框架」——這正是這幾輪你不斷要求我把 SKILL.md 寫得更精確（domain decision、free access 二次攔截、低分備選警示）所反映的缺口。
- **適合沉澱成哪些概念**：見下方「建議 concept note」。
- **可能連到哪些專案**：weekly-reading-ingest 本身、Ricky-KnowledgeBase 的 `.claude/skills/kb-*` 系列 skill 設計慣例。
- **限制或風險**：文章引用的具體工具/repo（如 oh-my-claudecode 19 個智能體）屬於快速變動的生態，半年後可能過時；concept note 應只保留決策框架本身，避免把易過時的工具清單寫成「結論」。

## 風險與限制

- 三篇皆為真實搜尋結果但僅完成單次 WebFetch 驗證，未做交叉比對其他獨立來源，concept note 若要產生應標記 `confidence: medium`。
- Main Pick 作者背景資料有限（僅知 X/Twitter handle @gyakuse），無法進一步驗證其專業背景，屬於個人部落格而非機構發表。
- Backup B 為 preprint，尚未確認是否經過同行評審。
- Backup A 明確觸發 domain 規則邊界情況，本報告刻意保留它作為候選，用來驗證 `DOMAIN_DECISION` 流程在真實場景下是否合理——這是測試目的之一，不代表它本身品質不足。

## 建議產生的 Concept Note（假設選 Main Pick）

- `agentic-workflow-selection-matrix`（依專案規模/驗證方式選擇 workflow 的決策矩陣）— domain 草案：`ai-workflow`
- `context-engineering-failure-modes`（context engineering 常見失敗模式與緩解策略）— domain 草案：`ai-workflow`
- `agents-md-design-checklist`（AGENTS.md / SKILL.md 設計檢查清單：文件大小、驗證規則、分層載入）— domain 草案：`ai-workflow`

## 可能的 Project Link

- **weekly-reading-ingest**：本工具目前的 `.claude/skills/weekly-reading-curate(/ingest)/SKILL.md` 可直接用文章的「AGENTS.md 設計檢查清單」（文件大小 60–150 行、驗證規則、分層載入）自我檢查，是否要精簡或分層尚待你決定。
- **Ricky-KnowledgeBase**：既有 `.claude/skills/kb-*` 系列 skill 的設計慣例，可與本文的「會話設計複雜度光譜」對照，評估目前 10 個 kb skill 是否有過度複雜或可合併的部分（僅為觀察，非本輪要做的事）。
- portfolio-tracker / movie-app：本週沒有明確專案連結。

## Free Access 判斷依據

| 候選 | Free Access | 依據 |
|---|---|---|
| Main Pick | Yes | 作者個人部落格直接公開全文，無付費牆、無註冊牆 |
| Backup A | Yes | 作者個人筆記網站直接公開，無付費牆 |
| Backup B | Yes | arXiv 公開預印本，CC BY 4.0 授權，永久免費 |

三篇皆為 Yes，本次未出現付費牆或不明候選；`FREE_ACCESS_CHECK`（若進入 ingest 階段）預期可直接通過，不會觸發攔截。

## 互動選項

1. 確認主選
2. 改選備選 A
3. 改選備選 B
4. 補連結後重評
5. 重新搜尋
6. 本週跳過
