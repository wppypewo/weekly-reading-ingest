# Weekly Reading Candidates — 2026-W27

status: AWAITING_CONFIRMATION
generated_at: 2026-07-01
mode: strict（curate 階段兩模式相同）

## 本週主題判斷

- **預設主題**：AI 代理 / 個人自動化工具的工程化穩健性（從「即時合成」走向可版本化、可信任的工作流）
- **選題理由**：對照 `schema/context/current-focus.md`——目前明確記載的下階段焦點是「修復工具穩定性、路徑可遷移性（Mac 遷移）、processed 策略、strict/quick 模式」，且 `README.md` 明文「暫不建議立刻掛 routine；建議先手動跑 2–3 週確認會持續使用，並完成路徑可遷移性與穩定性修復後再開」。本週三篇候選分別從「設計框架」「評估科學」「個人實踐反思」三個角度切入這個待決策情境。
- **是否使用手動連結**：否，本次未收到使用者提供的連結。
- **是否含當週熱門內容**：否，三篇皆為 2026 年內的研究論文 / 部落格文章，非本週爆紅內容；已如實標註非熱點。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | Engineering Robustness into Personal Agents with the AI Workflow Store |
| Author | Roxana Geambasu, Mariana Raykova, Pierre Tholoniat, Trishita Tiwari, Lillian Tsai, Wen Zhang（Google / Columbia University） |
| Source | arXiv preprint 2605.10907 |
| URL | https://arxiv.org/abs/2605.10907 |
| Language | English |
| Estimated Reading Time | 約 35–45 分鐘（全文 13 頁，含案例與圖示） |
| Type | Paper（設計 / 立場論文，非同行評審 preprint） |
| Free Access | Yes（arXiv 開放取用） |
| Topic | ai-workflow — 個人 AI 代理的工程化穩健性設計 |

**五項評分**

| 軸 | 分數 | 說明 |
|---|---|---|
| Source Quality | 4 | Google + Columbia 研究者，機構可信，但屬設計提案，缺乏大規模實證數據 |
| Idea Density | 4 | 版本控制 / 監控 / 隔離 / 復原四層防禦，結構清晰、案例具體 |
| Long-term Value | 4 | 提出可重用的個人代理穩健性框架，非一次性資訊 |
| Relevance | 5 | 直接對應 `weekly-reading-ingest` 專案「暫不掛 routine，待穩定性修復」的待決策情境 |
| Obsidian Fit | 4 | 可獨立沉澱為「個人代理穩健性四層防禦」概念頁 |

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | Towards a Science of AI Agent Reliability |
| Author | Stephan Rabanser, Sayash Kapoor, Peter Kirgis, Kangheng Liu, Saiteja Utpala, Arvind Narayanan |
| Source | arXiv preprint 2602.16666 |
| URL | https://arxiv.org/abs/2602.16666 |
| Language | English |
| Estimated Reading Time | 全文精讀約 60–90 分鐘（52 頁）；僅讀指標定義與結論約 20 分鐘 |
| Type | Paper（實證評測論文，非同行評審 preprint） |
| Free Access | Yes（arXiv 開放取用） |
| Topic | ai-engineering — AI 代理可靠性評測框架（12 項指標 / 4 維度：一致性、穩健性、可預測性、安全性） |

**五項評分**

| 軸 | 分數 | 說明 |
|---|---|---|
| Source Quality | 5 | 作者含 Princeton AI 可信度研究學者，方法嚴謹，14 模型 × 2 benchmark 實測 |
| Idea Density | 4 | 12 項具體指標，資訊量高，但 52 頁篇幅稀釋單頁密度 |
| Long-term Value | 4 | 可作為長期引用的評測詞彙庫 |
| Relevance | 3 | 偏學術評測框架，對本週待決策（工具該怎麼修）幫助較間接 |
| Obsidian Fit | 3 | 篇幅過長，若要完整沉澱需分次進行 |

**推薦理由**：與主選互補——主選給設計方案，本篇給「如何量化評估某個個人代理是否可信任」的詞彙與指標，可用來日後檢核 `weekly-reading-ingest` routine 是否真的準備好上線。因偏學術評測、不直接給設計決策，故列備選而非主選。

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | Code as a Tool of Process |
| Author | Jim Nielsen |
| Source | Jim Nielsen's Blog（個人部落格） |
| URL | https://blog.jim-nielsen.com/2026/code-as-process/ |
| Language | English |
| Estimated Reading Time | 5–7 分鐘 |
| Type | Article / Blog essay |
| Free Access | Yes |
| Topic | ai-workflow — AI 生成程式碼 vs 手寫程式碼：流程本身作為思考工具 |

**五項評分**

| 軸 | 分數 | 說明 |
|---|---|---|
| Source Quality | 3 | 資深獨立設計工程師的個人部落格，非機構研究，但業界口碑良好 |
| Idea Density | 3 | 短文、單一核心比喻（鎬鏟 vs 炸藥），資訊量不如兩篇論文 |
| Long-term Value | 3 | 個人實作習慣層級的提醒，非框架級貢獻 |
| Relevance | 4 | 直接呼應使用者高度依賴 Claude Code 的日常實作情境 |
| Obsidian Fit | 4 | 短小易沉澱，適合快速概念頁 |

**推薦理由**：作為輕量對照——補足兩篇長論文的閱讀負擔，且直接可套用在使用者每天用 Claude Code 寫程式的自我檢查上：哪些片段該親手寫過一次、哪些可以放心交給生成。

---

## 主選勝出理由

- **為何是主選**：直接對應 `current-focus.md` 明確記載的「下階段焦點」與 `README.md`「暫不掛 routine，待穩定性與可遷移性修復後再開」的待決策情境；文中四層防禦（版本控制 / 監控 / 隔離 / 復原）可直接轉譯成 `weekly-reading-ingest` curate→ingest 兩階段安全閘門的設計參考，是三篇中唯一能立即對應到「這週該怎麼修工具」的一篇。
- **為何勝過兩備選**：Backup A 學術嚴謹度更高，但屬評估科學、不提供設計方案,對本週實際決策幫助較間接；Backup B 短小精悍但格局限於個人程式碼撰寫習慣，層級小於主選涉及的系統設計問題。
- **補的知識缺口**：使用者目前缺乏「個人 agent 如何從手動半自動閉環走向可信任自動化」的結構化參考詞彙（workflow versioning、sandboxing、rollback）。
- **適合沉澱的概念**：「個人代理穩健性四層防禦模型」，可獨立成 reusable concept，未來可用於任何個人自動化專案，不限於本工具。
- **可能的專案連結**：weekly-reading-ingest 工具專案（README.md 明文待解決的 routine 穩定性問題）。

## 風險與限制

- Main Pick 與 Backup A 皆為未經同行評審的 arXiv preprint（2026 年新作），結論尚未經社群充分檢驗。
- Main Pick 屬設計提案，缺乏大規模實證數據，不能當作「已證明有效」的方案，只能當參考框架，實作前仍需自行驗證。
- Backup A 全文 52 頁，若之後改選它，實際 ingest 工作量會明顯高於預估，建議分次精讀。
- 三篇皆為英文原文，無中文版本，概念名詞需自行翻譯並在 concept note 標明原文。

## 建議產生的 concept note（標題草案）

- 「個人代理穩健性工程：從即時合成到版本化工作流」
- 或「AI Workflow Store 四層防禦模型（版本控制 / 監控 / 隔離 / 復原）」

## 可能的 project link

- weekly-reading-ingest（工具專案本身）——對應 README.md「暫不建議掛 routine，待穩定性與可遷移性修復」的待決策項。
- 註：是否同時連結 Ricky-KnowledgeBase 的 `tools/kb/*.mjs`（若未來要仿造 workflow store 的版本化思路）需要人工判斷，本報告不硬連，先只列前者。

## 互動選項

1. 確認主選
2. 改選備選 A
3. 改選備選 B
4. 補連結後重評
5. 重新搜尋
6. 本週跳過

---
（此檔案僅為候選報告存檔，未寫入 Obsidian vault；未收到上述三選一明確確認前不會觸發 `weekly-reading-ingest`。）
