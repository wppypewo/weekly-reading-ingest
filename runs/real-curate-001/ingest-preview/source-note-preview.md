---
# 預覽用 frontmatter，非正式 vault frontmatter
type: source
status: raw
domain: ai-workflow
source: 作者個人技術部落格
author: 逆瀬川ちゃん（Sakasegawa-chan, @gyakuse）
published: 2026-03（推估，依文章標註月份）
created: 2026-06-22
processed: false
confidence: medium
related_concepts: []
tags: [weekly-reading]
---

> 本檔為 ingest preview，**目標 folder：`raw/sources/articles/`**。本輪未實際寫入 vault。

# A Survey of Development Workflows in the Coding Agent Era（Preview）

## Source

- Title: A Survey of Development Workflows in the Coding Agent Era
- Author: 逆瀬川ちゃん（Sakasegawa-chan，@gyakuse）
- URL: https://nyosegawa.com/en/posts/coding-agent-workflow-2026/
- Language: English
- Source Type: 個人技術部落格 essay
- Free Access: Yes（作者個人部落格直接公開全文，無付費牆、無註冊牆）
- Estimated Reading Time: 約 25 分鐘

## Selected Short Excerpts（節錄，非全文，僅作引用線索）

> "in 2025 the question was 'can AI write working code?' but in 2026 the question is 'how do you orchestrate AI to ship production code?'"

## 摘要（繁體中文重寫，非逐句翻譯）

文章主張軟體開發已進入「智能體工程」時代：開發者角色從寫程式碼轉為協調與監督 agent。提供 5 個結構化框架：(1) workflow 選擇矩陣（依專案規模/驗證方式選方法）、(2) context engineering 失敗模式表（8 類失敗模式與緩解策略）、(3) 會話設計複雜度光譜（從 1 行 bash 迴圈到 19 個智能體的複雜系統）、(4) AGENTS.md 設計檢查清單（核心建議：文件大小 60–150 行、驗證規則含路徑存在性檢查與 ADR 過期偵測（5 天閾值）、分層載入 L1 元資料／L2 指令／L3 資源三層）、(5) 權限最小化清單（工具權限、MCP 驗證、密鑰隔離、破壞性操作阻止）。核心立場：人機協作應在明確審查點介入，而非持續監控。

## 我的閱讀理由

本週實際工作正是設計 `weekly-reading-curate` / `weekly-reading-ingest` 兩個 Claude Code skill 文件，文中的 AGENTS.md 檢查清單與會話複雜度光譜可直接拿來自我檢查現有兩份 SKILL.md 的設計品質，是目前最貼近實務缺口的一篇。

## 候選評分（來自 candidates.md）

- Source Quality: 4/5 — 作者原站發表，含具體案例與框架，但屬個人技術部落格，非同行評審
- Idea Density: 5/5 — 提供至少 5 個結構化決策框架，密度極高
- Long-term Value: 3/5 — 引用具體工具/repo（如 19 個智能體的 oh-my-claudecode），半年後部分細節可能過時
- Relevance: 5/5 — 直接對應本週實際在做的事
- Obsidian Fit: 4/5 — 可拆成多個獨立 concept，domain 落在既有 `ai-workflow` 無疑義

## Caveats

- 作者身份未完全獨立驗證：僅知 X/Twitter handle `@gyakuse`，無法確認真實姓名、機構背景或專業資歷。
- 文章屬個人技術 essay，**非同行評審研究**，論點未經第三方審查。
- 部分工具 / repo / workflow 名稱（例如特定 agent 數量、特定工具組合）屬快速變動生態，**可能快速過時**，concept note 應只保留決策框架本身，不寫入易過時的工具清單細節。

## 處理紀錄

- 2026-06-22：建立 source note preview（尚未寫入 vault）

## 後續可萃取概念（暫不獨立 ingest，留待未來需要時再評估）

- workflow 選擇矩陣（依專案規模/驗證方式選擇開發 workflow）
- context engineering 失敗模式表（8 類失敗模式與緩解策略）

> 本輪只 ingest `agents-md-design-checklist` 一個 concept（見 `concept-note-preview.md`），上述兩項先記錄在此，不重複拆成獨立 concept note。

## Next Actions（若使用者正式確認 ingest）

1. 寫入 `raw/sources/articles/2026-W26-coding-agent-era-workflow-survey.md`（檔名待確認週次格式）
2. 寫入 1 篇 concept note 到 `wiki/concepts/ai-workflow/agents-md-design-checklist.md`
3. 寫入 1 篇 project-link note 到 `wiki/outputs/weekly-reading/project-links/`
4. 寫入 1 篇 review-card 到 `wiki/outputs/weekly-reading/review-cards/`
5. 追加 `meta/weekly-reading/log.md`
6. 呼叫 `npm run kb:index`
