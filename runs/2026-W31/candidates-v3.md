# 2026-W31 每週精讀候選報告（v3）

產出日期：2026-07-31
模式：strict（預設）
狀態：AWAITING_CONFIRMATION

> v1 三篇（ai-workflow）全數退回；v2 主選為 3,500 字專欄，經判定撐不起精讀深度。
> 本輪為 concept note 深度規格（8,000 字下限）訂立後的第一份報告，採新格式：每篇加 **Source Weight**，主選加 **深度可行性**。
> 依 `FAILURE-HANDLING.md` A 區規則，不覆寫 v1／v2。

---

## 本輪的規格變更（已確認後執行，未 commit）

| 檔案 | 變更 |
|---|---|
| `curate/SKILL.md`（含 `.agents` Codex 版） | 新增必填 **Source Weight** 欄位；主選新增**深度可行性**欄位。來源不設厚度門檻，但撐不起 8,000 字者須附回溯文獻清單，缺清單不得為主選 |
| `ingest/SKILL.md`（含 `.agents` Codex 版） | 新增「concept note 深度規格」整節：不得短於 source note／≥ 8,000 字／必填章節與覆蓋要求／必含 `## 我的辨證`。新增薄來源處理與禁止灌水條款。狀態機加 `DEPTH_CHECK` |
| vault `templates/concept-note.md` | 新增 `## 我的辨證` 章節（唯一動到的 vault 檔案，事前已確認） |

---

## 本週主題判斷

- **預設主題**：親密關係的可預測邊界——我們自以為能解釋和預測關係好壞的那些變數，實際上能做到多少。
- **選題理由**：
  - v2 暴露的問題是「來源撐不起精讀」。本輪直接往高密度實證研究走，而非再找一篇有觀點但薄的評論。
  - 主選同時能接上 vault 既有的一條線。`llm-judge-self-inconsistency`（評分者不穩定）與 `harness-induced-belief-divergence`（執行環境不中立）講的都是「我們以為測得到的東西其實測不到」。本篇把同一個問題搬到人際關係場域，且結論更硬。這是跨 domain 的真連結，不是硬連。
- **是否使用手動連結**：否，全部為自動搜尋。
- **是否含當週熱門內容**：否。主選為 2020 年論文，見「風險與限制」第 1 點。
- **同質性聲明**：主選屬 psychology，兩篇備選屬 sociology，兩個新 domain 都有代表。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | Machine learning uncovers the most robust self-report predictors of relationship quality across 43 longitudinal couples studies |
| Author | Samantha Joel、Paul W. Eastwick 等（共 86 位關係科學研究者，29 個實驗室） |
| Source | PNAS 117(32): 19061–19071（同行評審） |
| URL | https://www.pnas.org/doi/10.1073/pnas.1917036117　／　免費全文：https://pmc.ncbi.nlm.nih.gov/articles/PMC7431040/ |
| Language | English |
| Estimated Reading Time | 約 120–150 分鐘（統計密集，另有補充材料） |
| **Source Weight** | **11 頁（19061–19071）＋ 補充材料（Supplementary Information）** |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（PMC7431040 免費全文，已實讀） |
| Topic | 關係品質、可預測性、自陳測量的邊界 |
| Domain | psychology ✓（本輪新增，在 `allowedConceptDomains` 內） |

### 深度可行性（新規格必填）

**撐得起 8,000 字，無須外補材料。** 依據：四組變異量對照（actor/partner × relationship/individual）、兩張各 10 項的預測力排序表、一個重大 null result、一個「變化不可預測」的結論、作者明列的四項理論約束、五項自陳限制。單是把這些逐一展開並保留原始數值，就足以達標。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 5 | PNAS 同行評審；43 個資料集、29 個實驗室、86 位研究者、39 筆資助整合而成。這是本工作流至今出現過的最高等級來源 |
| Idea Density | 5 | 2,413 項基線測量、1,149 個關係變數、每資料集 21 個模型；四組變異量對照 + 兩份排序表 + 兩個 null result |
| Long-term Value | 5 | 作者明列的「對未來理論的四項約束」是結構性結論，不隨模型或時代失效 |
| Relevance | 4 | 直接對應新增的親密關係主題。扣分處：與使用者現有專案無操作性關聯 |
| Obsidian Fit | 5 | 可開 `psychology` domain，且能與既有兩篇概念接成「測量與可預測性的邊界」跨領域線 |

**Main Pick 軟門檻檢查**：Source Quality 5 ≥ 3 ✓／Relevance 4 ≥ 3 ✓／Free Access = Yes ✓／domain ∈ allowedConceptDomains ✓ → 通過。

### 全文要點（已實讀 PMC 全文）

**規模**：基線 22,163 人、11,196 對伴侶、43 個縱貫資料集、29 個實驗室。平均 4 個時間點、橫跨 14 個月（範圍 2–11 點、2–48 個月）。基線收集 2,413 項自陳測量，其中 1,149 個為關係特定變數。

**方法**：Random Forests，每個模型 5,000 棵回歸樹，`mtry` 用預設（預測變數的三分之一），以 VSURF 套件做變數篩選，用 out-of-bag 樣本估計樣本外表現。每個資料集跑 21 個模型（預測基線滿意度、追蹤滿意度、滿意度變化），含承諾變數的資料集另跑 21 個。

**預測力排序（成功率）**

| 關係特定變數 | | 個人差異變數 | |
|---|---|---|---|
| 感知伴侶承諾 | 85% | 生活滿意度 | 88% |
| 親密感 | 81% | 憂鬱 | 74% |
| 感激 | 72% | 負向情感 | 73% |
| 愛 | 71% | 焦慮型依戀 | 71% |
| 性滿意度 | 71% | 逃避型依戀 | 70% |
| 感知伴侶滿意度 | 70% | 年齡 | 68% |
| 衝突 | 69% | 焦慮 | 66% |
| 感知伴侶回應性 | 69% | 自尊 | 58% |
| 信任 | 68% | 親和性 | 54% |
| 投入 | 67% | 正向情感 | 54% |

**變異量解釋**

| 變數組合 | 基線滿意度 | 追蹤滿意度 |
|---|---|---|
| 自己報告的關係變數 | **45%** | **18%** |
| 自己報告的個人變數 | 19% | 12% |
| 伴侶報告的關係變數 | 15% | 7% |
| 伴侶報告的個人變數 | 5% | 5% |
| 全部合併 | 44% | — |

**兩個關鍵結論**

1. **全部合併（44%）沒有超過「只用自己報告的關係變數」（45%）。** 作者原文：任何由自己的個人差異、伴侶的個人差異、伴侶的關係特定變數所解釋的變異，都能被自己的關係特定變數解釋掉。作者舉的例子是：若 Amir 與 Alex 各自填了大量關於自身與關係的問卷，**Amir 的關係品質中所有可預測的部分，都只由他自己對這段關係的感受解釋**；他自己的特質、Alex 的特質、Alex 對關係的感受，全都不再增加任何解釋力。
2. **關係品質的「變化」幾乎無法預測。** 所有分析都解釋不到 5% 的變異，且所有估計的信賴區間大幅重疊。作者：關係將會變好或變壞的任何早期訊號，似乎都不存在於基線的自陳變數裡。

**作者自陳限制**
- 全部資料來自西方國家（美、加、瑞士、紐西蘭、荷蘭、以色列），跨文化外推未經檢驗。
- **99.4% 為明確的自陳評分量表**，而非直接捕捉實時行為的獨立觀察。作者建議未來納入觀察資料與情境變數，並具體點名報稅資料、日間皮質醇節律、他人評定。
- 心理學實驗室的資料集比例高於社會學、傳播、家庭研究，該學科偏誤可能導致不同結論。
- 樣本同質性疑慮（雖已納入刻意過採低收入族群的 Supporting Healthy Marriages Project）。
- 作者明言變化不可預測「很可能是因為變化取決於外部情境、行為歷程，或其他本身也在變動的因素」。

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | What Is Social Connection in the Context of Human Need: An Interdisciplinary Literature Review |
| Author | Kyla L. Bauer、Rachel Johnson-Koenke、Meredith P. Fort（皆為 University of Colorado Anschutz Medical Campus） |
| Source | International Journal of Environmental Research and Public Health（MDPI，2025-03-01） |
| URL | https://pmc.ncbi.nlm.nih.gov/articles/PMC11941835/ |
| Language | English |
| Estimated Reading Time | 約 90–120 分鐘 |
| **Source Weight** | **約 12,000–14,000 英文字** |
| Type | paper |
| Free Access | **Yes**（CC BY 4.0，已實讀） |
| Topic | 社會連結的跨學科定義、人類需求、統一概念模型 |
| Domain | sociology ✓ |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 2 | MDPI 期刊的審查品質長年受質疑；且**非系統性回顧**——44 篇核心文獻為 purposive 迭代選取，作者自承不窮盡 |
| Idea Density | 4 | 橫跨 11 個學科、萃取 9 個共通概念、提出統一概念模型與新定義，概念量確實大 |
| Long-term Value | 3 | 概念統整型工作，價值取決於後續是否被採用，目前未知 |
| Relevance | 3 | 對應人際連結主題，但停在定義層，不提供機制也不給可操作結論 |
| Obsidian Fit | 3 | 定義與框架適合沉澱，但證據等級低，須標 `confidence: low` |

### 推薦理由

它處理的是主選跳過的問題：**社會連結到底是什麼**。作者主張社會連結是與食物、水、住所同級的生存必需，透過恆定與生理機制運作；跨社會神經科學、公共衛生、生態學等領域萃取出九個共通概念（演化、資源、環境、生態系、暴露科學、體現、恆定、異位負荷理論、跨學科取徑），並提出把社會連結與氧氣、水、食物、住所並列的統一模型。

厚度足夠（12,000–14,000 字），但方法等級明顯低於主選。作者自陳的限制相當坦白：未檢視社會連結定義的多元文化差異、未充分處理公衛的公平性優先議題、可能仍偏生物學視角；且諮詢的 30 位專家中 21 位回覆，過程中出現族群健康專家與社會科學家之間「明顯的張力」。

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | How studying friendship has changed the way I understand my own loneliness |
| Author | Marie-Elisabeth Lei Pihl（哥本哈根大學傳播系博士後） |
| Source | The Conversation（外刊，CC-BY，2026-05-15） |
| URL | https://theconversation.com/how-studying-friendship-has-changed-the-way-i-understand-my-own-loneliness-281767 |
| Language | English |
| Estimated Reading Time | 約 20–30 分鐘 |
| **Source Weight** | **約 3,500 英文字** |
| Type | article |
| Free Access | **Yes** |
| Topic | 友誼的社會位階、孤獨、社會腳本 |
| Domain | sociology ✓ |

> v2 的主選，依你的指示保留但降為備選。評分沿用 v2（Source Quality 3／Idea Density 3／Long-term Value 4／Relevance 4／Obsidian Fit 4），要點見 [`candidates-v2.md`](candidates-v2.md)。

### 依新規格的深度可行性判定：**撐不起，且回溯清單不完整**

這正好是新規格第一次實際咬到東西。3,500 字要撐起 8,000 字的 concept note，必須回溯其引用的原始文獻，但清單湊不齊：

| 需回溯的來源 | 狀態 |
|---|---|
| Hartup & Stevens 的友誼研究（「不到清醒時間的 10%」） | 可定位，尚未取得全文 |
| Putnam《Bowling Alone》 | 可定位，專書 |
| 「超過 40% 成年人希望有更親近友誼」的美國調查 | **原文未給出處，我目前無法定位** |
| 「每週不到 3 小時 vs 十年前 6 小時」 | **原文未給出處**（方向與 BLS 美國時間運用調查一致，但確切數字對不上） |

依 `curate/SKILL.md` 新增條款，**缺完整回溯清單的薄來源不得列為 Main Pick**。若要改選此篇為主選，需先補齊上述兩項出處。

---

## 主選勝出理由

- **為何是主選**：這是本工作流至今遇到的最高等級來源，且它的結論不是「多一個相關性」，而是**劃出一條邊界**——告訴你自陳測量在親密關係上能做到什麼、做不到什麼。精讀的價值密度最高的一種文本就是這種。
- **為何勝過 Backup A**：A 厚度夠、概念量也大，但它是 purposive 選取 44 篇文獻的非系統性回顧，發表在審查品質受質疑的期刊，且停在定義層。主選是 43 個縱貫資料集的整合分析，證據等級差了不只一級。
- **為何勝過 Backup B**：B 有觀點但只有 3,500 字，依新規格連主選資格都沒有——而且它引用的兩個關鍵數據我連原始出處都定位不到。這件事本身就說明了為什麼要立這條規格。
- **補的知識缺口**：vault 六個 concept domain 至今沒有一篇處理人與人的關係。這是開一個從未存在的面向，且是用最硬的證據開場。
- **適合沉澱的概念**：「關係品質的可預測邊界」——你自己對這段關係的感受幾乎解釋了所有可解釋的部分；伴侶怎麼想、你們各自是什麼樣的人，加進來不增加任何解釋力；而關係會變好還是變壞，從自陳資料裡看不出來。
- **可能的專案連結**：**本週沒有明確專案連結。** 五個專案全為技術性專案，不硬連。

---

## 風險與限制

1. **主選是 2020 年論文，非近期內容**。精讀規則未要求時效，且此篇屬於整合型里程碑研究、老化較慢，但其後五年可能已有新的複驗或反駁，ingest 時應查一次後續引用狀況並在 concept note 標注。
2. **全部資料來自西方國家**，跨文化外推未經檢驗——對使用者所處脈絡的適用性需明確保留。
3. **99.4% 為自陳量表**。這點必須寫進 concept note 且不能輕輕帶過：「變化不可預測」這個結論，究竟是關係變化本身不可預測，還是**自陳量表測不到它**，論文無法分辨。作者自己把它歸因於外部情境與行為歷程，等於承認是後者的可能性。這是全篇最需要小心解讀的地方。
4. **學科偏誤**：心理學實驗室資料集佔比高於社會學、傳播、家庭研究，作者自陳可能因此得出不同結論。
5. **Backup A 的期刊與方法品質問題**（MDPI、非系統性回顧），若改選須標 `confidence: low`。
6. **Backup B 依新規格已無主選資格**，回溯清單有兩項無法定位。
7. **兩個新 domain 仍為空目錄狀態**。依 vault 2026-06-28 決策不預建，ingest 時才由 `/kb-ingest` 建立。
8. **ingest 時的深度連鎖要求**：新規格要求 concept note **不得短於 source note**，且 ≥ 8,000 字。本篇資訊量大，source note 若寫得完整很可能超過 5,000 字，concept note 必須再高於它。這會讓本輪 ingest 明顯比前三輪耗時，請先有預期。

---

## 建議產生的 concept note（標題草案）

- 路徑：`wiki/concepts/psychology/relationship-quality-predictability-limits.md`
- 中文標題草案：**關係品質的可預測邊界：自己的感受解釋一切，而變化幾乎測不到**
- 與既有筆記的關係：可與 [[wiki/concepts/ai-engineering/llm-judge-self-inconsistency]]、[[wiki/concepts/ai-engineering/harness-induced-belief-divergence]] 接成一條跨 domain 的「測量與可預測性的邊界」線——三者都在講「我們以為測得到的東西，其實測不到」。這是 vault 第一次出現跨 domain 的概念線。

---

## 可能的 project link

**本週沒有明確專案連結。** 不硬連。

---

## 互動選項

1. **確認主選** — Joel et al. 2020, PNAS：關係品質的可預測邊界（psychology）
2. **改選備選 A** — Bauer et al. 2025：社會連結的跨學科定義（sociology，注意期刊與方法品質）
3. **改選備選 B** — The Conversation：友誼與孤獨（**注意：依新規格無主選資格，需先補齊兩項出處**）
4. **補連結後重評**
5. **重新搜尋**
6. **本週跳過**

> 確認後才進入 `weekly-reading-ingest`。ingest 前另有一項需你單獨批准：是否更新 vault 的 `wiki/concepts/README.md`（新增 `psychology` / `sociology` 條目），該檔屬 KnowledgeBase 既有檔案。
