# 2026-W31 每週精讀候選報告（v2）

產出日期：2026-07-31
模式：strict（預設）
狀態：AWAITING_CONFIRMATION

> v1（[`candidates.md`](candidates.md)）三篇候選全被退回。使用者指示：新增外刊作為候選管道，主題新增社會學、人際關係、親密關係、心理學。
> 依 `FAILURE-HANDLING.md` A 區規則，同週重跑不覆寫 v1，另存本檔。

---

## 本輪已執行的 config 變更（已確認後執行，未 commit）

| 檔案 | 變更 |
|---|---|
| `weekly-reading.config.json` | `vaultRoot` 由 `D:/ClaudeCode/...` 改為 `/Users/ricky/ClaudeCode/KnowledgeBase/Ricky-KnowledgeBase` |
| `weekly-reading.config.json` | `allowedConceptDomains` 新增 `psychology`、`sociology`（現為六個） |
| `README.md` §6 | 白名單文字同步（順帶移除早已失效的 `design`）；新增「候選來源管道」小節，載明外刊為新增管道之一、非主要來源、不因刊物身分加減分 |

未變更：`freeOnly` 維持 `true`、`allowedSourceFolders` 維持四項、`mainPickThreshold` 全部不動。

---

## 本週主題判斷

- **預設主題**：社交連結的衰退——把它同時當成社會結構問題與個人心理機制問題來看。
- **選題理由**：本輪是 `sociology` / `psychology` 兩個 domain 首次啟用，刻意選能各自立住的方向，而非硬找一篇跨兩者的文章。主選走社會學（友誼在社會腳本中的位階），備選 A 走心理學（依戀安全如何轉譯成不孤獨的機制），兩者互為對照：一個講結構，一個講個體。
- **是否使用手動連結**：否，全部為自動搜尋。
- **是否含當週熱門內容**：否。主選為 2026-05-15，備選 A 為 2026-02-11。本週未追熱門。
- **同質性聲明**：三篇分屬 sociology（主選、備選 B）與 psychology（備選 A），已脫離連續兩輪的 ai-workflow 單一 domain 狀態。

### 外刊管道啟用狀況（首次，需記錄）

- 主選即為外刊（The Conversation，CC-BY）。
- **Aeon 連續三次回 HTTP 429**，三篇原本鎖定的 essay（loneliness / 被愛卻孤獨 / care 與 scare）全部無法取得全文。依規則不得靠摘要或二手描述評分，故本輪未列入任何 Aeon 文章。
- 這是外刊管道的第一個實務障礙：**部分外刊會限制自動抓取**。若你希望 Aeon 進入常態候選池，之後可由你直接貼連結（互動選項 4），或改在別的時段重試。
- 付費牆外刊（The Economist / New Yorker / The Atlantic / FT）本輪未納入搜尋，符合 `freeOnly: true`。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | How studying friendship has changed the way I understand my own loneliness |
| Author | Marie-Elisabeth Lei Pihl（哥本哈根大學傳播系博士後研究員） |
| Source | The Conversation（外刊，學術作者專欄，CC-BY） |
| URL | https://theconversation.com/how-studying-friendship-has-changed-the-way-i-understand-my-own-loneliness-281767 |
| Language | English |
| Estimated Reading Time | 約 20–30 分鐘（約 3,500 字） |
| Type | article → `raw/sources/articles/` |
| Free Access | **Yes**（全文開放，CC-BY 授權） |
| Topic | 友誼的社會位階、孤獨、社會腳本 |
| Domain | sociology ✓（本輪新增，在 `allowedConceptDomains` 內） |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | 作者有明確學術身分與機構，The Conversation 有編輯把關且 CC-BY。但這是科普專欄非同行評審研究，且文中數據皆為二手轉述 |
| Idea Density | 3 | 一個清楚主張 + 四組量化數據 + 文學案例。3,500 字的密度中等，不到論文級 |
| Long-term Value | 4 | 「友誼被社會腳本降級為餘裕」這個框架不依賴時效數據，十年後仍可用 |
| Relevance | 4 | 本輪三個新方向（外刊／社會學／人際關係）唯一同時滿足的一篇。扣分處：與使用者現有專案無操作性關聯 |
| Obsidian Fit | 4 | 主張清楚、可獨立沉澱，適合作為 `sociology` domain 的開篇。扣分處：需回溯原始文獻才能寫得紮實 |

**Main Pick 軟門檻檢查**：Source Quality 3 ≥ 3 ✓／Relevance 4 ≥ 3 ✓／Free Access = Yes ✓／domain ∈ allowedConceptDomains ✓ → 通過。

### 全文要點（已實讀全文）

**作者處境**：Pihl 具備社會意義上的完整配置——婚姻、子女、丹麥郊區自有住宅——卻仍感到一種物質條件無法填補的匱乏。她把自身經驗與友誼研究、文學分析並置。

**核心主張**：現代社會運行在一套限縮的社會腳本上，優先序是事業 → 婚姻 → 家庭，友誼被降級為次要項目。這個位階安排本身製造了存在層次的飢餓感。她主張友誼應具備同等的**結構性**重要性，而不只是生活的餘裕。

**引用數據（皆為二手轉述）**：
- 心理學者 Hartup 與 Stevens：成人在事業與家庭負荷最重的階段，與朋友相處的時間**不到清醒時間的 10%**。
- 一項美國研究：**超過 40%** 的成年人希望擁有情感上更親近的友誼。
- 美國人每週與朋友相處**不到 3 小時**，十年前是 6 小時。
- 政黨、宗教組織、工會、社團的參與率同步下滑（引 Putnam《Bowling Alone》）。

**文學框架**：以 Édouard Louis、Thomas Korsgaard 的作品呈現友誼作為讓人脫離既定出身的轉化力量；並舉 Selma Lagerlöf、Virginia Woolf 的女性友誼如何支撐非典型人生。

**作者提出的實踐方向**：把友誼理解為「實踐」而非「擁有」；主動建立跨世代連結；經營日常互動中的弱連結；把友誼的定義擴大到傳統模型之外。

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | Serial mediation pathways linking attachment security to loneliness: the role of self-disclosure quality and perceived social support among college students |
| Author | Hong Guo（陝西師範大學／成都理工大學）、Qian Zhu（成都中醫藥大學）、Yikun Zhong（西南石油大學）、Wei Huang（西華師範大學） |
| Source | Frontiers in Psychology（同行評審期刊，OA） |
| URL | https://doi.org/10.3389/fpsyg.2026.1749281 |
| Language | English |
| Estimated Reading Time | 約 60–80 分鐘 |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（Frontiers 全 OA，HTML 全文已實讀） |
| Topic | 依戀安全、自我揭露、感知社會支持、孤獨 |
| Domain | psychology ✓（本輪新增） |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | 有同行評審與明確機構，但 Frontiers 的審查嚴謹度長年有爭議；無預先註冊 |
| Idea Density | 3 | 單一序列中介模型，路徑係數具體，但概念維度少，全篇環繞一條鏈 |
| Long-term Value | 2 | 橫斷面 + PROCESS 中介設計，這類結論在複驗中常大幅縮水；本身不是可長期依靠的知識 |
| Relevance | 4 | 直接對應新增的親密關係／依戀主題，且提供的是**機制**而非現象描述 |
| Obsidian Fit | 3 | 可沉澱成「依戀安全如何轉譯成不孤獨」的機制筆記，但須標 `confidence: low` |

### 推薦理由與數據

N = 1,098 名中國大學生（平均年齡 20.15，SD 1.28；**女性佔 82.9%**），PROCESS Model 6，5,000 次 bootstrap。模型解釋孤獨感變異的 **43.2%**。

三條顯著的間接路徑，佔比差距很大：
- 只經由**感知社會支持**：B = −0.433，佔總間接效果 **69.5%**
- 完整序列中介（依戀安全 → 自我揭露品質 → 感知社會支持 → 孤獨）：B = −0.110，佔 **16.9%**
- 只經由**自我揭露品質**：B = −0.084，佔 **13.6%**

值得注意的是分配本身：**保護作用幾乎七成集中在「感覺被支持」，而不是「說了多少」**。這對「多開口就會比較不孤獨」的直覺是一個修正。

**作者自陳限制**：橫斷面無法推論因果；只測整體孤獨，未區分情緒性與社會性孤獨；全為自陳量表；女性佔比過高限制外推；中國文化脈絡的跨文化適用性存疑。

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | Uneven access to essential services and amenities: Geographic disparities in 'third place' availability across the United States from 2010 to 2021 |
| Author | Yue Sun, Michael H. Esposito, Mallory Sagehorn, Robert A. Melendez, Jessica M. Finlay |
| Source | Health & Place, Vol. 96（Elsevier，同行評審） |
| URL | https://doi.org/10.1016/j.healthplace.2025.103583 |
| Language | English |
| Estimated Reading Time | 未知（未取得全文） |
| Type | paper |
| Free Access | **No**（ScienceDirect 僅開放摘要；PubMed 未提供 PMC 免費全文連結；未找到作者自存版或其他免費替代版） |
| Topic | 第三場所、社會基礎設施、地理不平等 |
| Domain | sociology ✓ |

> **依 curate 規則，Free Access = No 不得列為 Main Pick，本篇只能列備選。** 且我未能實讀全文，以下評分僅根據摘要，可信度低於另外兩篇。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 既有同行評審期刊，五位作者，NETS 資料庫 + 廣義加性混合模型，方法交代清楚 |
| Idea Density | 3 | 僅摘要層級可判斷：12 類場所 × 三個社會維度的變化，資訊量應該不低，但無法確認 |
| Long-term Value | 4 | 「社交衰退首先是基礎設施問題」這個結構性框架，比個體心理解釋更耐久 |
| Relevance | 3 | 對應社會學主題，但全為美國資料，對使用者所處脈絡的適用性需另行判斷 |
| Obsidian Fit | 1 | **付費牆 + 未實讀全文，現階段無法沉澱成概念筆記**——這是最低分的直接原因 |

### 推薦理由

它提供的是主選缺的那一半。主選把孤獨歸因於社會腳本與個人選擇，本篇則指出**場所本身在消失**：以 Census tract 層級資料檢視 2010–2021 年 12 類第三場所（畫廊、理髮店、社團、咖啡店、速食店、雜貨店、圖書館、電影院、博物館、休閒中心、餐廳、老人中心）的變化，發現 **2019–2021 全部 12 類都出現大規模關閉**，且衰退在社會弱勢人口集中的 tract 與鄉村地區特別劇烈。

若要改選此篇為主選，必須先解決全文取得問題，且需重新評估 Free Access——目前狀態不符合主選門檻。

---

## 主選勝出理由

- **為何是主選**：它是三篇裡唯一同時滿足你這次提出的三個新條件——外刊、社會學、人際關係——且全文可讀、授權清楚（CC-BY，引用無虞）。作為 `sociology` domain 的第一篇，方向設定的意義大於單篇資訊量。
- **為何勝過 Backup A**：A 的方法透明度更高、數字更硬，但它回答的是一個窄問題（依戀安全經由哪條路徑降低孤獨），且設計等級（橫斷面自陳中介）決定了結論的暫定性。主選提供的是一個能組織後續閱讀的**框架**，而不是一個待複驗的係數。
- **為何勝過 Backup B**：B 的結構性視角其實最有價值，但它卡在付費牆且我未能實讀——依規則連主選資格都沒有。
- **補的知識缺口**：vault 目前六個 concept domain 全是工具性或學術技術性的（AI 工程、AI 工作流、軟體工程、金融、法文、文化理論），**沒有任何一篇處理人如何與人相處**。這不是補一個細節，是開一個從未存在的面向。
- **適合沉澱的概念**：「友誼作為結構，而非餘裕」——把友誼從「有空才經營的附加品」重新定位成與事業、家庭同級的生活基礎設施，並指出這個降級是社會腳本造成的，不是個人意志薄弱。
- **可能的專案連結**：**本週沒有明確專案連結。** `wiki/projects/` 下五個專案全為技術性專案，與本篇無實質關聯，不硬連。依 strict mode，project-link preview 本輪可不產（`MODES.md` 對 quick mode 有明文，strict mode 下建議同樣處理，但需你裁示）。

---

## 風險與限制

1. **主選的所有數據都是二手轉述**。「不到清醒時間的 10%」「超過 40%」「每週不到 3 小時 vs 十年前 6 小時」在原文都沒有完整出處。若確認主選，**寫進 concept note 前必須回溯 Hartup & Stevens 原始研究與那份美國調查**，否則會把專欄的轉述當成一手數據存進 vault。這是本輪最大的品質風險。
2. **主選是科普專欄，不是研究**。Source Quality 只有 3，與 W29 那篇 preprint 同級。它的價值在框架不在證據強度。
3. **主選帶有明顯的個人敘事與規範性立場**（作者本人的處境、對社會腳本的批評）。沉澱時須把「作者的主張」與「引用的證據」分開標示，不可混寫成客觀結論。
4. **備選 A 的樣本偏差嚴重**：82.9% 為女性、全為中國大學生、橫斷面設計。若採用，`confidence` 必須標 low，且不得寫成因果陳述。
5. **備選 B 付費牆且未實讀**，評分可信度低於另外兩篇，Obsidian Fit 只有 1 分。
6. **Aeon 抓取失敗（連續三次 429）**，外刊管道首次啟用即遇到取得性障礙，本輪候選池因此比預期窄。
7. **兩個新 domain 都是空的**。`wiki/concepts/sociology/` 與 `wiki/concepts/psychology/` 目前不存在——這是預期狀態。依 vault `wiki/concepts/README.md` 2026-06-28 決策，**不預先建立空資料夾**，資料夾應在 ingest 實際寫入時才由 `/kb-ingest` 建立。ingest 階段不得為了「先把結構做好」而建空目錄。
8. **`wiki/concepts/README.md` 需要更新**（新增 domain 條目），但該檔在 vault 內，屬「未經確認不得修改 KnowledgeBase 既有檔案」的範圍。**若確認主選，這會是 ingest 階段需要你單獨批准的一項**，我不會順手改。

---

## 建議產生的 concept note（標題草案）

- 路徑：`wiki/concepts/sociology/friendship-as-structure.md`
- 中文標題草案：**友誼作為結構，而非餘裕：社會腳本如何把人際連結降級**
- 與既有筆記的關係：目前 vault 內**無任何可連結的既有概念**。這是 `sociology` domain 的第一篇，也是全 vault 第一篇處理人際關係的筆記。若日後採納備選 A，可與之組成「結構層 × 個體機制層」的概念對。

---

## 可能的 project link

**本週沒有明確專案連結。** 不硬連。

---

## 互動選項

1. **確認主選** — The Conversation：友誼與孤獨（sociology）
2. **改選備選 A** — Frontiers：依戀安全 → 孤獨的序列中介（psychology）
3. **改選備選 B** — Health & Place：第三場所消失（注意：付費牆，須先解決全文取得，且不符主選門檻）
4. **補連結後重評** — 你直接貼外刊連結（例如 Aeon 那幾篇），與現有候選混合評分
5. **重新搜尋** — 換方向或換刊物
6. **本週跳過**

> 確認後才會進入 `weekly-reading-ingest`。ingest 前另有兩項需你單獨批准：是否更新 vault 的 `wiki/concepts/README.md`、strict mode 下是否略過 project-link preview。
