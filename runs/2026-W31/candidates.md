# 2026-W31 每週精讀候選報告

產出日期：2026-07-31
模式：strict（預設）
狀態：AWAITING_CONFIRMATION

---

## 執行前警示（需使用者決策，**未擅自修改**）

1. **`weekly-reading.config.json` 的 `vaultRoot` 仍是 Windows 路徑** `D:/ClaudeCode/KnowledgeBase/Ricky-KnowledgeBase`，該路徑在 Mac 上不存在。
   - 本階段（curate）不寫 vault，本次 vault context 直接讀 `/Users/ricky/ClaudeCode/KnowledgeBase/Ricky-KnowledgeBase`，故 curate 不受影響。
   - 但**下一階段 ingest 會踩空**。確認主選前後須先決定是否把 `vaultRoot` 改為 `/Users/ricky/ClaudeCode/KnowledgeBase/Ricky-KnowledgeBase`。
2. **2026-W30 無 run 紀錄**（`runs/` 只有 W26、W27、W29）。本輪為 W29 之後的第一次策展，中間隔一週。

---

## 本週主題判斷

- **預設主題**：倉庫層 context file（AGENTS.md / CLAUDE.md）到底有沒有用——把「寫指令檔」這件事本身當成待驗證的假設。
- **選題理由**：
  - `schema/context/current-focus.md` 的下階段焦點是「工具專案穩定性、路徑可遷移性」，而使用者整個工作區建立在多層指令檔上（全域 `~/.claude/CLAUDE.md` + `rules/` + 工作區根 `CLAUDE.md` + 各 repo 自有 CLAUDE.md）。
  - vault 首篇精讀沉澱的概念就是 [[wiki/concepts/ai-workflow/agents-md-design-checklist]]——那是「該怎麼寫」的規範性內容，至今沒有任何「寫了到底有沒有效」的實證對照。本週刻意找反證。
  - 同時延續 W29 建立的「評估效度」線：[[wiki/concepts/ai-engineering/llm-judge-self-inconsistency]]（評分者不穩定）→ [[wiki/concepts/ai-engineering/harness-induced-belief-divergence]]（執行環境不中立）→ 本週（配置檔效益未經驗證）。
- **是否使用手動連結**：否，全部為自動搜尋。
- **是否含當週熱門內容**：主選 v1 為 2026-02，v2 修訂於 2026-06-23，非當週新內容；本週未刻意追熱門。
- **候選同質性聲明**：三篇候選同屬 ai-workflow / ai-engineering。本週在 finance domain 找到一篇方向合適的（SSRN「The Growth and Consequences of Index Investing」，2026-01），但 SSRN 頁面回 403 無法讀取，Free Access 判定為 `Unclear` 且無法實讀，依規則不得列為主選，也不硬塞進備選——故本週維持單一 domain。這是 W29 已標示過的同一個風險，連續兩輪未解。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents? |
| Author | Thibaud Gloaguen, Niels Mündler, Mark Müller, Veselin Raychev, Martin Vechev |
| Source | arXiv（preprint，未見同行評審紀錄；v1 2026-02-12，v2 2026-06-23） |
| URL | https://arxiv.org/abs/2602.11988 |
| Language | English |
| Estimated Reading Time | 約 90–120 分鐘（24 頁） |
| Type | paper |
| Free Access | **Yes**（abs / PDF 全開放） |
| Topic | context file 效益、agent 配置、評估方法論 |
| Domain | ai-workflow ✓（在 `allowedConceptDomains` 內） |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 五位作者，Raychev / Vechev 為 ETH Zurich 系統與程式分析領域已知研究者，且已修訂至 v2。扣分原因：仍是 preprint，未見同行評審紀錄 |
| Idea Density | 4 | 兩個 benchmark（其一自建）、四種 agent × 模型組合、instructions 與 repository overview 分開量測。扣分原因：核心結論單一，多數篇幅在支撐同一個主張 |
| Long-term Value | 4 | 「context file 的效益必須實測，不能靠廠商建議」這個方法論主張可長期沿用；具體數字會隨模型換代失效 |
| Relevance | 5 | 使用者整個工作區靠多層指令檔運作，且 vault 已有一篇規範性 concept note 沒有實證對照 |
| Obsidian Fit | 5 | 可與 `agents-md-design-checklist` 構成「主張 vs 反證」對照，並直接接上既有的評估效度概念群 |

**Main Pick 軟門檻檢查**：Source Quality 4 ≥ 3 ✓／Relevance 5 ≥ 3 ✓／Free Access = Yes ✓／domain ∈ allowedConceptDomains ✓ → 通過，無須人工決策標記。

### 全文要點

> **取材說明**：v2 的 arXiv HTML 版不存在（404），以下數字取自 **v1 HTML 全文**；abs 頁顯示的 v2 摘要（「does not generally improve task success rates, while increasing inference cost by over 20% on average」）與 v1 數字方向一致。若確認主選，ingest 前應以 v2 PDF 逐項核對數值。

**設定**
- Agent × 模型：Claude Code + Sonnet-4.5／Codex + GPT-5.2／Codex + GPT-5.1 mini／Qwen Code + Qwen3-30b-coder。
- Benchmark 一：SWE-bench Lite，300 個任務，來自 11 個熱門 Python repo，搭配 **LLM 生成**的 context file。
- Benchmark 二：**AGENTbench（作者自建）**，138 個 instance，來自 12 個 niche Python repo，全部含**開發者實際 commit 的** context file；由 5,694 個 PR 篩選而來。

**主要數據**
- LLM 生成的 context file：SWE-bench Lite 平均解題率**下降 0.5%**，AGENTbench 平均**下降 2%**。
- 成本：LLM 生成的 context file 使步數增加，平均成本上升 **20%（SWE-bench Lite）／23%（AGENTbench）**。
- **開發者手寫**的 context file：**除 Claude Code 外的所有 agent 都有改善**，整體平均約 **+4%**；成本上升至多 19%。
- Instructions vs Overview 拆解：
  - 指令**確實會被遵守**——context file 提到 `uv` 時，平均每個 instance 使用 1.6 次；未提到時低於 0.01 次。
  - Repository overview **無效**——兩個 benchmark 上，context file 的存在都沒有顯著減少 agent 接觸到相關檔案前所花的步數。

**作者自陳的限制**
- 評估高度集中在 Python。
- 先前 benchmark 的 instance 本身沒有 context file（故需自建 AGENTbench）。
- 只量測 task resolution rate，未涵蓋程式效率或安全性影響。
- AGENTbench 相對 SWE-bench Lite 樣本偏小。

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | Instruction Adherence in Coding Agent Configuration Files: A Factorial Study of Four File-Structure Variables |
| Author | Damon McMillan |
| Source | arXiv（preprint，CC BY 4.0，2026-05-11；cs.SE / cs.CL） |
| URL | https://arxiv.org/abs/2605.10039 |
| Language | English |
| Estimated Reading Time | 未知（未取得頁數，見下方註記） |
| Type | paper |
| Free Access | **Yes**（PDF 開放，CC BY 4.0） |
| Topic | 配置檔結構、指令遵從度、session 內衰減 |
| Domain | ai-workflow ✓ |

> **實讀狀態：未實讀全文。** arXiv HTML 版不存在（404），PDF 文字抽取失敗，以下僅為 abs 頁摘要內容。若改選此篇為主選，須先解決全文取得問題（例如本機下載後轉文字）。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 2 | 單一作者、abs 頁未見機構標示、preprint 未經同行評審。加分點僅在實驗量體與開放授權 |
| Idea Density | 3 | 主要產出是一個 null result 加一個 session 內衰減發現，維度偏少 |
| Long-term Value | 3 | 「結構變數不重要、位置衰減才重要」若成立則有價值，但目前是單一未複驗來源 |
| Relevance | 4 | 直接在 Claude Code CLI 上實測，對象就是使用者每天在用的工具 |
| Obsidian Fit | 3 | 適合作為主選 concept note 的佐證段落，單獨成篇證據強度不足 |

### 推薦理由

規模不小：1,650 個 Claude Code CLI session、16,050 筆 function-level 觀測。兩個結果都反直覺——
（1）四個檔案結構變數與三個雙向交互作用，**經多重檢定校正後全部測不出差異**；
（2）真正顯著的是 session 內行為：agent 每多生成一個 function，遵從機率的勝算約**下降 5.6%**。

若成立，含意是「CLAUDE.md 怎麼排版不重要，重要的是 session 拉長後指令會被稀釋」。這與主選的「instructions 會被遵守、overview 沒用」是互補而非重複的一刀。但作者背景不明、且我尚未實讀全文，證據強度明顯低於主選。

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | Harness Engineering for Agentic AI Coding Tools: An Exploratory Study |
| Author | Matthias Galster, Seyedmoein Mohsenimofidi, Jai Lal Lulla, Muhammad Auwal Abubakar, Christoph Treude, Sebastian Baltes |
| Source | arXiv（preprint，CC BY 4.0；v1 2026-02-16，v5 2026-06-30） |
| URL | https://arxiv.org/abs/2602.14690 |
| Language | English |
| Estimated Reading Time | 約 40–50 分鐘（10 頁） |
| Type | paper |
| Free Access | **Yes**（PDF 開放，CC BY 4.0） |
| Topic | agent 配置機制生態、AGENTS.md 標準化、skills / subagents 採用率 |
| Domain | ai-workflow ✓ |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 六位作者，Treude / Baltes / Galster 為軟體工程實證研究領域常見作者；已修訂至 v5、CC BY。扣分原因：preprint |
| Idea Density | 3 | 描述性 landscape study：八種配置機制分類 + 採用率統計，無因果推論也無效能量測 |
| Long-term Value | 2 | 生態快照，工具版本迭代後很快過時 |
| Relevance | 3 | 可定位使用者自身在生態中的位置，但不改變任何決策 |
| Obsidian Fit | 2 | 描述性統計難沉澱成一則有主張的 concept note |

### 推薦理由

分析 2,853 個 GitHub repo，涵蓋 Claude Code、GitHub Copilot、Cursor、Gemini、Codex 五種工具。三個發現：
（1）Context File 主導整個配置生態，常是 repo 內唯一機制，**AGENTS.md 正在成為跨工具的互通標準**；
（2）Skills 與 Subagents 採用率很低，且 Skills 多半只放靜態指令而非可執行腳本；
（3）不同工具長出不同配置習慣，**Claude Code 使用者使用的機制種類最廣**。

對使用者的直接意義：目前的做法（多層 CLAUDE.md + 自建 skills + `.agents/` 對照版本）在統計上屬於極少數。此篇能提供「我在哪」的座標，但提供不了「該不該這樣做」的答案——這也是它評分最低的原因。

---

## 主選勝出理由

- **為何是主選**：它是三篇裡唯一有對照組、有成本量測、且結論能直接改變使用者行為的。它不是告訴你「怎麼寫指令檔」，而是先問「寫了有沒有用」，並把答案拆成兩半：**指令有用、倉庫概述沒用**。
- **為何勝過 Backup A**：A 的相關性同樣高（直接測 Claude Code），但作者背景不明、單一來源、且我尚未實讀全文；主選是五人團隊、已修訂至 v2、自建 benchmark 並公開數據路徑。證據強度不同級。
- **為何勝過 Backup B**：B 只描述「大家都在用什麼」，不回答「有沒有用」。在使用者已經深度使用這些機制的前提下，描述性統計的邊際價值很低。
- **補的知識缺口**：vault 現有 `agents-md-design-checklist` 是規範性的（該怎麼寫），完全沒有效益驗證的一面。主選補上反面證據，讓那則概念筆記從「建議」升級成「有條件的建議」。
- **適合沉澱的概念**：「倉庫層 context file 的淨效益」——效益不是布林值，要按 **內容類型（指令／概述）× 作者（開發者手寫／LLM 生成）× agent** 三個維度拆開看，且必須把 token 成本計入。
- **可能的專案連結**：`skill-portability`。該實驗的結論是「內容層可移植，執行層會放大內容層錯誤」；主選則顯示「指令被忠實執行、概述被忽略」。兩者放在一起可推進到更精確的說法：**執行層放大的是被實際遵守的那部分內容，而非全部內容**。

---

## 風險與限制

1. **主選是 preprint，未經同行評審**，Source Quality 給 4 而非 5。引用數據時須標明來源狀態。
2. **版本不一致風險**：數字取自 v1 HTML，最新是 v2（2026-06-23）。ingest 前須以 v2 PDF 核對，若有出入以 v2 為準。
3. **摘要與內文有張力，不得只抄摘要**：摘要說「不普遍改善」，但內文顯示**開發者手寫**的 context file 對 Claude Code 以外的 agent 平均改善約 4%。摘要是把 LLM 生成與開發者手寫合併陳述的結果。沉澱 concept note 時必須保留這個區分，否則會寫出比論文本身更強的結論。
4. **樣本侷限**：全 Python；SWE-bench Lite 300 instances + AGENTbench 138 instances；只量測解題率，不含效率與安全性。
5. **Backup A 未實讀全文**，其數字目前只有摘要層級可信度。
6. **候選同質性**：三篇全屬 ai-workflow。W29 已標示過同一風險，本輪仍未解——finance / french 兩個 domain 連續兩輪掛零。
7. **利益相關性提醒**：主選的結論若成立，直接指向使用者現有的長篇 CLAUDE.md（全域規則檔數千字、含大量 repository overview 性質的內容）。這是本篇對使用者價值最高、也最容易讀成自我否定的地方——沉澱時建議只採「哪類內容有效」的結構性結論，不做工作區改造的即時決策。

---

## 建議產生的 concept note（標題草案）

- 主標：`wiki/concepts/ai-workflow/context-file-net-effect.md`
- 中文標題草案：**倉庫層 context file 的淨效益：指令有效、概述無效、成本必須計入**
- 與既有筆記的關係：對 [[wiki/concepts/ai-workflow/agents-md-design-checklist]] 加上實證邊界條件；與 [[wiki/concepts/ai-engineering/harness-induced-belief-divergence]] 同屬「配置與環境不是中性的」這條線。

---

## 可能的 project link

`wiki/projects/skill-portability/` — 主選的「指令被遵守、概述被忽略」可與該實驗「內容層可移植、執行層放大內容層錯誤」對接。

> 注意：`skill-portability` 已於 2026-07-18 標記完結，且寫入紅線規定**不得在 `wiki/projects/<project>/` 新增檔案**。若確認主選，project-link 應寫入 `wiki/outputs/weekly-reading/project-links/2026-W31-*.md`（與 W26、W29 一致），不動專案目錄本身。

---

## 互動選項

1. **確認主選** — Evaluating AGENTS.md
2. **改選備選 A** — Instruction Adherence（注意：須先解決全文取得問題）
3. **改選備選 B** — Harness Engineering
4. **補連結後重評** — 提供連結，與現有候選混合評分
5. **重新搜尋** — 換方向（例如指定 finance / french 以打破同質性）
6. **本週跳過**

> 確認後才會進入 `weekly-reading-ingest`，且需先處理上方 `vaultRoot` 路徑問題。
