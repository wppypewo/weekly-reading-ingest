# 2026-W32 每週精讀候選報告

產出日期：2026-08-09
模式：strict（預設）
狀態：AWAITING_CONFIRMATION

> 本週為 W31 兩篇（psychology）之後的第一輪。W32 目錄為新建，無同週重跑覆寫問題。
> 三篇候選皆已實際抓取全文（非僅 abstract），數值均取自原文。

---

## 本週主題判斷

- **預設主題**：CLI 編碼代理的實際效果——當「產出變多」與「品質變差」同時被測到時，該相信哪一組數字。
- **選題理由**：
  - 你每天在用 Claude Code，但 vault 裡關於「這東西到底有沒有用、代價是什麼」沒有任何一篇實證研究。`ai-workflow` domain 目前只有 1 篇 concept（`agents-md-design-checklist`），是全 vault 最空的活躍 domain。
  - 主選與備選 A 是同一問題的兩組矛盾答案：一篇說合併 PR +24%、四個月不衰減；另一篇說速度提升只出現在「代理是第一個 AI 工具」的專案，而且認知複雜度全面上升 35–43%。兩篇都是 2026 年、都用因果推論方法、結論衝突。
  - 這條矛盾接得上 vault 既有的一整條線：[[wiki/concepts/ai-engineering/llm-judge-self-inconsistency]]（評分者不穩定）、[[wiki/concepts/ai-engineering/harness-induced-belief-divergence]]（執行環境不中立）。三者問的是同一件事——**我們用來證明工具有效的那個測量，本身可不可信**。主選的作者是微軟員工、研究對象是微軟自家工具、結論對微軟自家產品有利，且作者在 positionality 章節自己承認了這點。這不是硬連，是同一個問題的第三個場域。
- **是否使用手動連結**：否，全部為自動搜尋。
- **是否含當週熱門內容**：主選為 2026-07-03 arXiv 預印本，屬近期內容；備選 A 為 2026-01；備選 B 為 2026-04。
- **同質性聲明**：主選與備選 A 同屬 `ai-workflow`，重疊度高（刻意如此，兩者互為對照）。備選 B 為 `sociology`，該 domain 至今 0 篇 concept。若你想避開 AI 工具主題，直接選 B。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | Adoption and Impact of Command-Line AI Coding Agents: A Study of Microsoft's Early 2026 Rollout of Claude Code and GitHub Copilot CLI |
| Author | Emerson Murphy-Hill、Jenna Butler、Alexandra Savelieva（皆為 Microsoft） |
| Source | arXiv 預印本 2607.01418v1（cs.SE / cs.AI / cs.HC），**未經同行評審** |
| URL | https://arxiv.org/abs/2607.01418 ／ HTML 全文 https://arxiv.org/html/2607.01418v1 |
| Language | English |
| Estimated Reading Time | 約 90–110 分鐘（五個 RQ、多組迴歸表、三條公式） |
| **Source Weight** | **23 頁**，含 10 張圖表、3 條計量模型方程式、609 份開放式問卷回應 |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（arXiv，CC BY 4.0，已實讀 HTML 全文） |
| Topic | CLI 編碼代理的採用、留存、產出效果 |
| Domain | ai-workflow ✓（在 `allowedConceptDomains` 內） |

### 深度可行性

**撐得起 6,000 字，不需回溯外部材料。** 依據：

- 五個研究問題各有獨立結果：RQ1 初始採用（5 組預測變數、各 3–4 個分層係數）、RQ2 留存（同結構，且方向與 RQ1 相反）、RQ3 產出（CausalImpact + 劑量反應兩套設計）、RQ4 工具比較、RQ5 亞群異質性。
- 可展開的硬數值超過 40 個，全部帶信賴區間。
- Threats to Validity 分構念／內部／外部三類，加一節作者 positionality 自陳，本身就是一整節可辨證的材料。
- 一個現成的內部矛盾：RQ1 說「IDE Copilot 老手更會去試 CLI（+83%）」，RQ2 說「同一群人留存率反而低 12–15%」。作者對此只給了一句推測。

**建議一併對照**（非必要，屬加值）：備選 A 的品質數據，用來檢驗主選「合併 PR」這個代理指標的效度。若採用，回溯清單為 arXiv 2601.13597v2（約 10–12 頁）。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | **arXiv 預印本，未經同行評審**；作者三人皆為 Microsoft 員工，研究對象含 Microsoft 自有產品。資料規模與方法嚴謹度高（含安慰劑檢定），但利益關係明確，因此不給 4 以上 |
| Idea Density | 5 | 五個 RQ、兩套獨立因果設計、40+ 個帶 CI 的效果量、609 份質性回應、一個未解釋的內部矛盾 |
| Long-term Value | 3 | 單一公司、單一 16 週窗口、2026 年初的工具世代。工具迭代快，具體數字兩年內會過時；但「用什麼指標證明工具有效」這個方法論問題不會過時 |
| Relevance | 5 | 研究對象就是你每天在用的工具，研究情境（既有 IDE Copilot 使用者轉用 CLI 代理）與你的實際路徑吻合 |
| Obsidian Fit | 4 | 直接落 `ai-workflow`（最空的活躍 domain）；能與現有兩篇 ai-engineering concept 形成第三個節點。扣分在於它偏「實證結果」而非「概念」，需要你自己抽出可長期保存的概念層 |

**總分 20 / 25**

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | AI IDEs or Autonomous Agents? Measuring the Impact of Coding Agents on Software Development |
| Author | Shyam Agarwal、Hao He、Bogdan Vasilescu（Carnegie Mellon University） |
| Source | arXiv 預印本 2601.13597v2（cs.SE），未經同行評審 |
| URL | https://arxiv.org/abs/2601.13597 ／ 複現包 https://github.com/shyamagarwal13/agentic-coding-impact |
| Language | English |
| Estimated Reading Time | 約 60–75 分鐘 |
| **Source Weight** | **約 10–12 頁**（會議論文格式），含事件研究圖、傾向分數匹配表、DiD 結果表 |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（arXiv，已實讀） |
| Topic | 編碼代理對開源專案速度與品質的因果效果 |
| Domain | ai-workflow ✓ |

**推薦理由**：方法比主選乾淨——錯開採用 DiD、傾向分數匹配（AUC 0.92–0.99，1:3 配對）、Borusyak 插補估計、517 個處理倉庫對 679 個控制倉庫、2024-01 至 2025-11。結論比主選難聽也更誠實：Agent-First 專案提交數 +36.25%、新增行數 +76.59%，但 IDE-First 專案的速度效果不顯著（提交 +3.06%，新增行 −6.34%），且 t=6 時掉到 −35% 提交、−61% 新增行。品質則兩組都退步：靜態分析警告 +17.7% / +19.0%，認知複雜度 +34.9% / +42.9%。

**它為什麼不是主選**：篇幅只有主選一半，資料是開源倉庫層級而非工程師個人層級，離你的實際使用情境較遠。作者自陳平行趨勢在品質指標上「可能不完全滿足」，並要求把估計視為 ITT 而非完整因果證據。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 同為未評審預印本，但 CMU 軟工實證組、有公開複現包、方法交代完整、限制自陳誠實，且無產品利益關係 |
| Idea Density | 4 | 三個 RQ、四類品質指標、AF/IF 異質性拆解；但數值組數約為主選一半 |
| Long-term Value | 4 | 「速度紅利只給沒用過 AI 的專案、複雜度成本人人有份」是結構性結論，比具體百分比耐放 |
| Relevance | 4 | 高度相關，但單位是專案倉庫而非個人開發者 |
| Obsidian Fit | 4 | 同樣落 `ai-workflow`；獨立成篇稍嫌薄，作為主選的對照材料價值更高 |

**總分 20 / 25**

> 註：與主選同為 20 分。**總分相同不代表可互換**——主選勝出理由見下節，不以總分決定。

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | Algorithmic management in the global gig economy: an interdisciplinary systematic literature review and critical discourse analysis |
| Author | Bianca Ifeoma Chigbu（Walter Sisulu University，南非） |
| Source | Frontiers in Sociology, Vol. 11（2026-04-15），**同行評審期刊** |
| URL | https://www.frontiersin.org/journals/sociology/articles/10.3389/fsoc.2026.1743445/full |
| Language | English |
| Estimated Reading Time | 約 100–120 分鐘 |
| **Source Weight** | **約 15,000–18,000 字**（Frontiers 系統性綜述常規長度）；分析 103 篇文獻（自 314 筆初篩）、35 份焦點文本、8 份政策文件 |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（Frontiers 全開放取用） |
| Topic | 演算法管理、平台勞動、勞動過程理論 |
| Domain | sociology ✓（在 `allowedConceptDomains` 內，**目前 0 篇 concept**） |

**推薦理由**：唯一一篇經同行評審的候選。三層概念框架（勞動過程與權力／演算法控制系統／制度與法律中介）加上論述分析的三種框架（技術樂觀、批判勞動、法律技術），是可以直接沉澱成 concept 的結構。它也順帶指出文獻本身的地理偏誤：歐洲 38%、北美 22%、非洲 7%、拉美 2%——一篇談「演算法如何管理全球零工」的文獻群，樣本卻集中在最不像零工經濟主戰場的兩個地區。

**它為什麼不是主選**：系統性綜述是二手材料，讀的是別人的發現而非原始資料。品質控制上作者自陳採單一評閱者篩選、未套用正式品質評分工具，這在 SLR 是明顯弱點。與你當前的專案與工具使用沒有直接關聯。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 同行評審期刊、PRISMA 流程、跨四個資料庫；扣分在單一評閱者、無品質評分工具 |
| Idea Density | 3 | 篇幅長但為綜述，觀點密度靠彙整而非原創發現；CDA 部分有真正的分析貢獻 |
| Long-term Value | 4 | 勞動過程理論與演算法控制的框架不隨技術世代失效 |
| Relevance | 2 | 與你當前專案、工作流、學習路徑都沒有直接接點；純屬拓寬 |
| Obsidian Fit | 3 | 能開 `sociology` 這個空 domain 的第一篇，但與 vault 現有節點幾乎無連結，短期會是孤島 |

**總分 16 / 25**

---

## 主選勝出理由

**為何是主選**：這是唯一一篇研究對象等於你日常工具、樣本單位等於「個人開發者」、而且量測期間涵蓋「從 IDE Copilot 轉向 CLI 代理」這條路徑的研究。你正好走在同一條路上。它給出的不只是「有沒有用」，而是「哪一種人會留下來用」——RQ2 的留存分析發現預測留存最強的是行為量（每週 2+ PR 者留存 +31%），而不是年資或職級。

**為何勝過備選 A**：A 的方法更乾淨，但單位是開源倉庫，看不到「人」。主選的 23 頁裡有五個 RQ 的完整結構加 609 份質性回應，撐 6,000 字綽綽有餘；A 只有 10–12 頁，獨立成篇要靠回溯補材料，反而不如當主選的對照材料好用。

**為何勝過備選 B**：B 的來源等級最高（唯一同行評審），但 Relevance 只有 2 分，且是二手綜述。主選是一手資料。

**補的知識缺口**：
1. `ai-workflow` domain 只有 1 篇 concept，是活躍 domain 中最空的。
2. vault 裡沒有任何一篇處理「AI 編碼工具的實證效果」——你有兩篇談 LLM 評估效度的 concept，但沒有一篇談你自己每天在用的工具實測起來怎樣。
3. 更重要的缺口是方法論：主選用「合併 PR 數」當唯一產出指標，備選 A 直接證明這個指標會漏掉品質退化。vault 現有的兩篇 concept 講的都是「測量不可信」，但都在 LLM 評估的場域內。這篇把同一個問題搬到「工程生產力指標」上。

**適合沉澱的概念**（標題草案）：
- 主推：`wiki/concepts/ai-workflow/coding-agent-productivity-proxy-gap`——編碼代理的產出提升與品質代價分別被不同指標捕捉，選哪個指標就決定了結論。
- 次選：`wiki/concepts/ai-workflow/agent-adoption-social-diffusion`——採用由同儕曝露驅動（跳級同儕 25%+ 使用 → 勝率 +216%），留存由個人行為量驅動；兩者的預測因子幾乎不重疊。

**可能的 project link**：本週沒有明確專案連結。現有五個專案（portfolio-tracker、movie-app、fashion-archive、personal-website、skill-portability）中，四個在 maintenance 或 completed，personal-website 尚未初始化，沒有一個以「AI 工作流本身」為主題。硬連到 weekly-reading-ingest 工具專案也不成立——那是工具，不是研究對象。

---

## 風險與限制

1. **主選未經同行評審**。arXiv 預印本，2026-07-03 上傳，尚無評審紀錄。source note 需明確標記，confidence 不得標 high。
2. **利益關係明確**。三位作者皆為 Microsoft 員工；Microsoft 擁有 GitHub、銷售 AI 工具。RQ4 的結論是「Copilot CLI 的提升是 Claude Code 的 2.2 倍」（+24.9% vs +11.4%）——即微軟自家產品勝出。作者在 positionality 章節承認「鄰近性可能形塑研究問題、設計與詮釋」，但未提供任何緩解措施。**這個結論在 concept note 中必須帶著這層脈絡引用，不得單獨摘出當事實。**
3. **產出指標單一**。全篇以「28 天內合併的 PR 數」為唯一產出量測，作者自陳「未測量品質、可能增加複雜性、可能偏好小而頻繁的 PR」。備選 A 的數據正好指向被漏掉的那一半。
4. **採用者自選偏誤**。CausalImpact 的處理組是自願採用者，合成反事實由未使用者建構。作者做了 2025-10-06 安慰劑檢定（−1.1%，CI 跨零）通過，但這只排除了時序假象，未排除選擇偏誤。
5. **劑量反應非因果**。Part 2 的 +15.0% → +50.1% 曲線，作者明說「高使用週可能含較輕的任務組合」，應視為關聯。
6. **外部效度窄**。單一公司、16 週、2026 年初的工具版本。你是個人開發者、非企業環境、無同儕曝露，RQ1 的社會擴散結論對你幾乎不適用。
7. **論文自身用 AI 撰寫**。作者披露以 GitHub Copilot（Claude Opus 4.6–4.8）產出初稿與全部分析程式碼。這不使結論失效，但在一篇評估 AI 工具效果的論文裡，值得在辨證章節記一筆。

---

## 互動選項

1. **確認主選** — Microsoft CLI 編碼代理 rollout 研究
2. **改選備選 A** — AI IDEs or Autonomous Agents（DiD 因果研究）
3. **改選備選 B** — 演算法管理與全球零工經濟（sociology 首篇）
4. **補連結後重評** — 提供你想加入的文章，與現有三篇一同評分
5. **重新搜尋** — 換主題方向
6. **本週跳過**

---

**狀態：AWAITING_CONFIRMATION。未收到上述明確確認語句前，不進入 ingest，不寫入 vault。**
