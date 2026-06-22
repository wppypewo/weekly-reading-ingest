# Weekly Reading Candidates｜DRY-RUN-001（假資料，未真實搜尋）

> 本檔案為 `weekly-reading-curate` skill 文件的 dry-run 測試輸出，所有文章、作者、URL 均為虛構，僅用於驗證候選報告格式與評分邏輯是否可執行。

## 本週主題判斷

- 預設主題：AI agent 的長期記憶與脈絡管理
- 選題理由：近期 portfolio-tracker 與 KB 都在處理「狀態如何跨 session 保存」，這個主題補的是 agent memory 設計缺口
- 是否使用使用者手動連結：否（本次全為模擬自動搜尋結果）
- 是否有當週熱門內容：Backup A 為熱門電子報內容，但僅因通過品質門檻才入選候選，熱度本身未加分

---

## Main Pick

- Title: Designing Durable Memory for Agents（假）
- Author: J. Rivera（假）
- Source: 作者個人技術 blog
- URL: https://example.com/durable-agent-memory
- Language: English
- Estimated Reading Time: 約 22 分鐘
- Type: Essay
- Free Access: Yes
- Topic: agent memory / context management

### Scores

- Source Quality: 4/5 — 作者原站發表，有實作背景佐證，非轉述他人觀點
- Idea Density: 5/5 — 單篇含多個可獨立複用的設計判準（分層記憶、失效策略、預算分配）
- Long-term Value: 4/5 — 屬架構層級概念，技術細節可能過時但設計判準可長期沿用
- Relevance: 5/5 — 直接對應本週「跨 session 狀態保存」缺口
- Obsidian Fit: 4/5 — 可拆成 2 個獨立 evergreen concept，邊界清楚不需大量改寫

### Why this is the main pick

補的是「記憶分層與失效策略」這個具體缺口；觀點密度高且可拆成可複用的 concept，與近期專案脈絡（狀態跨 session 保存）直接相關。

### Why it beats the backups

比 Backup A 觀點密度高出許多（A 偏新聞性轉述）；比 Backup B 更貼合本週實際缺口（B 理論價值高但本週相關性偏弱、閱讀成本也更高）。整體在「本週該讀什麼」這個判斷上，Main Pick 的 Relevance 與 Obsidian Fit 組合勝過兩篇備選的總分排序。

---

## Backup A

- Title: This Week in AI Agents（假）
- Author: 編輯部（假）
- Source: 熱門技術電子報
- URL: https://example.com/weekly-agents-roundup
- Language: English
- Type: Article
- Free Access: Yes
- Recommendation reason: 當週熱門、可掌握趨勢面，但屬彙整轉述性質，原始觀點密度偏低

### Scores

- Source Quality: 3/5 — 編輯彙整內容，非一手研究或實作經驗
- Idea Density: 2/5 — 多為新聞式條列，缺乏可獨立複用的判準
- Long-term Value: 2/5 — 時效性內容，數月後價值會明顯下降
- Relevance: 3/5 — 主題沾邊但未深入本週缺口
- Obsidian Fit: 2/5 — 內容鬆散，沉澱成 concept 需大量重新組織

---

## Backup B

- Title: A Formal Model of Context Windows（假）
- Author: arXiv preprint（假）
- Source: arXiv
- URL: https://arxiv.org/abs/0000.00000
- Language: English
- Type: Paper
- Free Access: Yes
- Recommendation reason: 理論深度與長期價值高，但與本週實際缺口的相關性、閱讀成本不如 Main Pick

### Scores

- Source Quality: 5/5 — 同行評審前的學術論文，方法論嚴謹
- Idea Density: 4/5 — 形式化定義扎實，但部分內容偏數學推導，可複用判準較少
- Long-term Value: 5/5 — 理論模型不易因實作細節變動而過時
- Relevance: 3/5 — 與本週「跨 session 狀態保存」實務缺口的直接關聯較弱
- Obsidian Fit: 3/5 — 需要額外轉譯才能變成可複用 concept，沉澱成本較高

---

## 風險與限制

- Main Pick 偏單一作者觀點，缺乏對照實證，concept note 應標記 `confidence: medium`
- Backup B 雖學術嚴謹，但本次未驗證是否已通過同行評審，僅為 preprint
- 三篇皆為假資料，本報告不代表任何真實內容判斷，僅用於測試 skill 文件可執行性

## 建議產生的 Concept Note

- `memory-layering-and-eviction`（記憶分層與失效策略）— domain 草案：`ai-engineering`
- `agent-context-budget`（脈絡預算）— domain 草案：`ai-engineering`

## 可能的 Project Link

- portfolio-tracker：跨 session 狀態保存的設計類比（需在 confirmed ingest 階段由使用者確認是否真有關聯，無則記「本週沒有明確專案連結」）

## 互動選項

1. 確認主選
2. 改選備選 A
3. 改選備選 B
4. 補連結後重評
5. 重新搜尋
6. 本週跳過
