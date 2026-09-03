# 2026-W33 每週精讀候選報告

產出日期：2026-08-16（週日）
模式：strict（預設）
狀態：AWAITING_CONFIRMATION

> W32 已於 `d1ac92a` 完成 ingest，W33 目錄為新建，無同週重跑覆寫問題。
> 三篇候選皆已實際抓取全文內容（非僅 abstract），數值均取自原文。
> 另有兩篇高度契合的純社會學文獻因取用受阻被排除，見文末「已檢視但排除」。

---

## 本週主題判斷

- **使用者指定**：親密關係 + 社會學，難度偏低。本週不由 Claude 自行決定方向。
- **選題理由**：
  - `sociology` 於 2026-07-31 加入 `allowedConceptDomains`，至今 **0 篇 concept**，是全 vault 唯一開了卻空著的 domain。
  - 親密關係在 vault 已有一篇：[[wiki/concepts/psychology/relationship-quality-predictability-limits]]（W31）。本輪必須避開重複——那篇談的是「關係品質測不出未來」，屬心理計量。本輪往社會結構層走。
  - 「難度偏低」在本流程有一個實際張力：ingest 的 concept note 有 6,000 字下限。所以本輪的選法是**讀起來輕、材料卻厚**——質性與論述分析優先，計量模型次之。
- **是否使用手動連結**：否，全部為自動搜尋。
- **是否含當週熱門內容**：主選為 2026-08-05 發表，距今 11 天，是三篇中最新的。
- **同質性聲明**：三篇分屬三種進路（論述分析／跨國計量／心理計量），不重疊。

### 一項需要你知道的 vault 不一致

`schema/context/current-focus.md` 第 48 行仍寫「concept domain 只用既有四個（ai-engineering / ai-workflow / finance / french）」，但 `weekly-reading.config.json` 的 `allowedConceptDomains` 已含 `psychology` 與 `sociology`，且 `wiki/concepts/psychology/` 實際已有 2 篇。這行描述已過時。**curate 階段不寫 vault，本輪不修**，僅回報給你決定何時處理。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | Can't help falling in love… with a bot? A mixed-methods analysis of public discourses of AI intimacy and companionship on YouTube |
| Author | Anurag Shekhar、Calvin Mabaso（University of Johannesburg，南非） |
| Source | Frontiers in Sociology, Vol. 11（2026-08-05），**同行評審期刊** |
| URL | https://www.frontiersin.org/journals/sociology/articles/10.3389/fsoc.2026.1846117/full |
| Language | English |
| Estimated Reading Time | 約 70–90 分鐘 |
| **Source Weight** | **約 18,000 字**，158 篇參考文獻；語料 8,757 則 YouTube 留言（其中 527 則進質性分析）；含 9 個 topic 的完整分佈表、10 種情緒的百分比與命中數 |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（Frontiers 全開放取用，已實讀全文） |
| Topic | AI 伴侶、親密關係的公共論述、承認與平台萃取 |
| Domain | sociology ✓（在 `allowedConceptDomains` 內，**目前 0 篇 concept**） |

### 為什麼它符合「不想太複雜」

方法是情感分析 + 情緒詞典 + 主題建模 + 反身性主題分析。前三項的輸出全是百分比與詞表，看表就懂；主要論證落在五個主題的敘事上，不需要統計訓練。相較之下備選 A 要讀跨層次交互作用、備選 B 要讀 bifactor 模型的 omegaH 與 ECV 指標。

### 深度可行性

**撐得起 6,000 字，不需回溯外部材料。** 依據：

- 五個主題各有 3–5 條子論證，且彼此有張力（主題 4 的「AI 只會附和」與主題 1 的「AI 比人安全」互相拉扯，作者自己點出這個矛盾）。
- 計量結果本身就是一整節可辨證的材料：情感分佈正面 38.86% / 負面 35.31% / 中性 25.83% 幾乎三分，作者據此主張這是**真實的矛盾心理而非共識**；NRC 情緒中信任 43.83% 與恐懼 35.69% 落在幾乎重疊的留言群上。
- 9 個 topic 的分佈可直接展開：Topic 1（一般關係語彙）獨佔 47.3%，Topic 7（宗教與求助語彙，god / jesus / help / lord）11.6% 自成一群，Topic 4 只講電影《Her》佔 3.5%。
- 三個理論框架各有具體落點：Honneth 的三種承認（親密之愛／法律尊重／社會尊嚴）、Zuboff 的萃取邏輯、Goffman 的污名作為邊界維持機制。另有 Bauman、Hochschild 作輔助。
- 一個現成的內部矛盾：作者一面用 Honneth 論證 AI 提供了被剝奪的承認，一面用 Zuboff 論證平台加深孤獨——同一套基礎設施同時是解方與病因。作者以 van Dijck & Poell 的「平台化親密」接合兩軸，但這個接合是否成立，是可以在 concept note 裡辨證的。

**加值回溯（非必要）**：若要把承認理論那一軸寫厚，可對照 Honneth《Struggle for Recognition》相關章節。不影響 6,000 字達標。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | 同行評審、方法交代完整、倫理程序明確。但資料是**單一影片下的 YouTube 留言**——發言者自選、身分不可驗證、可見性受演算法影響；且 Frontiers 為 APC 模式出版商，評審嚴謹度在學界有爭議。不給 4 以上 |
| Idea Density | 4 | 五主題各有子論證、9 個 topic、10 種情緒指標、三套理論落點、158 篇參考。扣分在相當比例是把既有理論套到留言上，原創發現的密度中等 |
| Long-term Value | 3 | 具體留言內容綁在 2026 年的 AI 伴侶產品世代，兩年內會過時；但「承認／萃取雙軸」與「孤獨是結構問題」兩個框架耐放 |
| Relevance | 4 | 直接命中你本週指定的親密關係 + 社會學；且接得上 [[wiki/concepts/psychology/ai-associated-delusions-amplification-spiral]]。扣分在與任何進行中的專案無關 |
| Obsidian Fit | 4 | 開 `sociology` 這個空 domain 的第一篇；五主題結構天然對應 concept note 的分節。扣分在該 domain 目前 0 篇，短期仍會是半孤島 |

**總分 18 / 25**

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | Sociodemographic and cultural factors are related to singlehood rates: A multilevel analysis across 59 countries from the World Values Survey |
| Author | Marta Kowal（University of Wrocław）、Katarzyna Adamczyk（Adam Mickiewicz University），波蘭 |
| Source | PLOS One, Vol. 20, Issue 10, e0335416（2025-10-29），同行評審 |
| URL | https://pmc.ncbi.nlm.nih.gov/articles/PMC12571265/ |
| Language | English |
| Estimated Reading Time | 約 60–75 分鐘 |
| **Source Weight** | **約 12,000–13,000 字**；資料為 World Values Survey 第七波（2017–2021），71,169 人、59 國 |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（CC BY 4.0，已實讀） |
| Topic | 單身率的個人與文化層次預測因子 |
| Domain | sociology ✓ |

**推薦理由**：這是三篇裡最「社會學」的一篇——把單身從個人選擇挪到人口與文化結構上。個人層次的方向有幾個違反直覺：教育程度**越高**越可能單身（log-odds 0.160）、收入越低越可能單身（−0.12）、失業增加單身機率（0.221），男性比女性更可能單身（−0.261）。國家層次上，個人主義越高（0.418）、彈性越低（−0.460）的社會單身率越高。最有價值的是跨層次交互作用：**個人因素的效果本身隨文化而變**——年齡×個人主義的效果量約 0.576，性別差異在個人主義國家更明顯。變異數解釋上，個人層次變數解釋 38.6%、國家層次僅 5.13%，但組內相關 22.3% 說明國家之間確實有實質差異。

**它為什麼不是主選**：橫斷面相關資料，作者明說無法判定因果方向。分析只涵蓋「從未結婚」者，排除離婚、分居、喪偶——這讓「單身」這個構念被切窄了。另外它是人口統計層次的描述，讀不到關係經驗本身，抽成 concept 時概念層較薄。複雜度也高於主選（跨層次模型 + 交互作用項）。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 同行評審、WVS 為公認權威跨國資料、樣本 71,169 人、CC BY、方法標準。扣分在 PLOS One 為方法導向而非選擇性期刊，且構念操作化偏窄 |
| Idea Density | 3 | 圍繞單一問題（誰單身、什麼社會條件下單身多），係數清楚但概念層薄；跨層次交互作用是全篇最有內容的部分 |
| Long-term Value | 4 | WVS 波段資料與文化維度框架不隨技術世代失效，結構性結論可長期引用 |
| Relevance | 3 | 命中親密關係 + 社會學，但單位是人口統計而非關係經驗，與你的處境與專案都無接點 |
| Obsidian Fit | 3 | 可落 `sociology`，但與 vault 現有節點幾乎無連結，且純計量描述不易抽出耐放的概念層，孤島風險高於主選 |

**總分 17 / 25**

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | Predicting relationship quality with itself? A single general factor captures most of the variance across 34 common relationship measures |
| Author | James J. Kim（Lakehead University）、Samantha Joel（Western University）、Paul W. Eastwick（UC Davis）、Thomas N. Bradbury、Benjamin R. Karney（UCLA）等 9 人 |
| Source | PLOS One, Vol. 21, Issue 4, e0342451（2026-04-01），同行評審 |
| URL | https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0342451 |
| Language | English |
| Estimated Reading Time | 約 120–150 分鐘 |
| **Source Weight** | **約 40,000–45,000 字**（含完整方法與補充材料）；兩個研究、N=3,439 人口普查配比樣本；Study 1 分析 206 題／27 構念，Study 2 分析 408 題／34 構念；資料公開於 OSF |
| Type | paper → `raw/sources/papers/` |
| Free Access | **Yes**（CC BY，已實讀） |
| Topic | 關係測量的構念重疊、情感壟斷（sentiment override） |
| Domain | psychology（**不是** sociology） |

**推薦理由**：全 vault 連結價值最高的一篇。W31 那篇（Joel 等人的 43 資料集整合分析）發現「自己對關係的感受解釋 45% 變異，加任何變數都不再增加」；這篇由**同一作者群**接著問：那 34 個號稱測不同東西的關係量表，是不是根本在測同一個東西？答案是：單一一般因子 Q 吃掉 73%（Study 1）到 82%（Study 2）的共同變異，各子因子的 omegaHS 全在 0.00–0.16 之間，遠低於 0.50 門檻。Q 與整體幸福感相關 0.61、與評價一致性偏誤相關 0.34。換句話說，W31 那個 45% 的天花板，這篇給出了機制解釋——不是關係測不準，是所有量表都在問同一個問題。

它同時接得上 vault 既有的「測量效度」那條線：[[wiki/concepts/ai-engineering/llm-judge-self-inconsistency]]、[[wiki/concepts/ai-engineering/harness-induced-belief-divergence]]、以及 W32 的 [[wiki/concepts/ai-workflow/coding-agent-productivity-proxy-gap]]。四篇問的是同一件事：**我們用來證明某件事的那個測量，本身測到了什麼**。這篇把它放進親密關係的場域。

**它為什麼不是主選**：**它違反你本週的兩項指定條件。** 一，主題是心理計量而非社會學，domain 只能落 `psychology`。二，它是三篇裡最複雜的——要讀懂核心結論得先理解 bifactor 模型、omegaH／omegaHS／ECV／ECVSS 四組指標的意義，全文 40,000 字以上，閱讀時間是主選的兩倍。它跟 W31 那篇的重疊也需要留意：不是重複，但 concept note 會有相當篇幅在處理兩者的關係。

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 作者群是關係科學核心人物（Karney、Bradbury、Eastwick、Joel）；兩個研究、人口普查配比樣本、OSF 公開資料、EFA/EBFA/CFA/CBFA 四套分析交叉驗證。扣分同 A：PLOS One 非選擇性期刊 |
| Idea Density | 4 | 34 個構念、兩研究、四組 bifactor 指標、sentiment override 的理論檢驗。扣分在論點集中——是同一結論被反覆嚴格驗證，而非多條獨立發現 |
| Long-term Value | 5 | 「關係科學的 34 個量表在測同一個東西」是動搖整個領域測量基礎的結論，且會改變你日後讀**任何**關係研究的方式。不隨時間失效 |
| Relevance | 3 | 命中親密關係，但不命中社會學；複雜度與你本週「不想太複雜」直接衝突。純以主題論相關性高，以本週條件論則被扣 |
| Obsidian Fit | 5 | 直接續寫 W31 的 concept，並把「測量效度」那條線從 AI 場域延伸到親密關係場域，形成第四個節點。全 vault 連結度最高 |

**總分 21 / 25**

---

## 主選勝出理由

**先講清楚一件事：備選 B 的總分（21）高於主選（18）。這不是誤植。**

依 SKILL 規範，主選不由總分決定。B 的分數高在 Long-term Value 與 Obsidian Fit——它對 vault 的結構價值確實是三篇裡最高的。但它同時違反你本週明確指定的兩項條件：不是社會學，而且是三篇裡最複雜的一篇（40,000+ 字、bifactor 模型、閱讀時間約主選兩倍）。**在你已經指定方向的一週，用總分把它推成主選是不對的。**

**為何是主選**：C 是唯一同時滿足「親密關係」「社會學」「讀起來不費力」三項的候選，且材料厚度足以撐起 6,000 字而不需回溯。它把親密關係放在一個你已經有素材的位置上——vault 已有 AI 與心理的一篇（AI 關聯妄想的放大螺旋），這篇補的是同一現象的社會學側面：不是個人為什麼會陷進去，而是這件事在公共討論中如何被合理化、被污名化、被商業化。

**為何勝過備選 A**：A 更「純社會學」，但讀到的是人口統計層次的係數，讀不到關係經驗本身；抽成 concept 時概念層薄，且與 vault 完全無連結。主選有五個主題結構、三套理論落點，以及一個真實的內部矛盾可辨證。

**為何勝過備選 B**：見上。B 的價值真實存在，但那是「等你想讀複雜東西的一週」的主選。

**補的知識缺口**：
1. `sociology` domain 開了 16 天仍是 0 篇，是全 vault 唯一開了卻空著的 domain。
2. vault 對親密關係只有一個切面——W31 的心理計量。缺結構與論述層面。
3. vault 有一篇談 AI 如何放大個人的妄想（psychology），但沒有一篇談**社會如何討論這件事**：誰被允許說 AI 陪伴是真的、誰會被叫作可悲、這個邊界由誰維持。主選的主題 2 與主題 4 正是這條。

**適合沉澱的概念**（標題草案）：
- 主推：`wiki/concepts/sociology/ai-intimacy-recognition-extraction-double-bind`——AI 伴侶同時是承認的來源與萃取的介面，兩者共用同一套平台基礎設施；把它當成單純的解方或單純的剝削都會漏掉一半。
- 次選：`wiki/concepts/sociology/loneliness-located-outside-the-self`——留言者系統性地把孤獨歸因於社群空間消失與連結商品化，而非個人失敗；這個歸因本身就是一個社會學現象。

**可能的 project link**：本週沒有明確專案連結。現有五個專案（robot-check、rot、portfolio-tracker、movie-app、personal-website）沒有一個以親密關係或社會學為題。robot-check 的「證明你不是機器人」與主選的「與機器人建立親密關係」之間只有修辭上的鄰近，不是概念關聯，**不建立 project-link**。

---

## 風險與限制

1. **分析對象是留言，不是關係經驗**。這篇研究的是「人們如何公開談論 AI 親密」，不是「AI 親密關係實際如何運作」。這是二階材料。concept note 全篇必須維持這個區分——作者自己在方法論上守住了這條線，摘錄時不得越界。
2. **引文經作者改寫以匿名化**。原文明載引用的留言為 author-modified for anonymity。這表示報告中所有「留言引文」都不是逐字原文，可驗證性受限。source note 需標記此點。
3. **單一影片、單一平台**。語料全部來自一支 60 Minutes Australia 影片下的留言。作者自陳該影片的敘事結構本身會形塑回應，且演算法決定了誰看到這支影片。這不是「公眾意見」，是特定討論串。
4. **詞典法無法辨識反諷**。VADER 與 NRC 都是詞典比對。在一個 Topic 6 明確標為「嘲諷與懷疑」（lol / wtf / scammers / demonic）的留言區裡，情感與情緒的百分比會被系統性扭曲。作者列了這項限制但未提出緩解措施。
5. **留言者身分完全不可驗證**。無法排除機器人、多帳號、行銷帳號。作者承認 commenter identity 與 user status 在經驗上不確定。
6. **理論框架的施加性**。用 Honneth 的承認理論與 Zuboff 的監控資本主義解讀 YouTube 留言，是研究者的詮釋，不是留言者的自陳。框架很可能比資料能支撐的更重。這點作者未充分處理，是 concept note 裡最值得辨證的一處。
7. **出版模式**。Frontiers 為 APC（作者付費）模式的開放取用出版商，其評審嚴謹度在學界有持續爭議。這不使本篇結論失效——方法與限制交代得相當完整——但 source note 的 confidence 不宜標 high。

---

## 已檢視但排除（誠實揭露）

以下兩篇在主題上比三篇候選更貼近「親密關係社會學」，但**無法取得全文**，依 FAILURE-HANDLING 規則不得列為 Main Pick，且不在僅憑摘要的情況下列入正式候選：

| 文獻 | 情況 |
|---|---|
| Denby & van Hooff (2026), *The couple paradox: The fantasy and failure of the couple norm in single and coupled lives*, **Sociology** | 主題極為契合：以 Berlant 的 cruel optimism 與 Scott 的 sociology of nothing 分析 28 位單身、18 位有伴侶者的生命史訪談。SAGE 站對本次抓取一律回傳首頁或 403，**Free Access 無法確認，標 `Unclear`**，全文未取得 |
| Twamley & van Hooff (2025), *Revitalising Intimacy Research Through a Focus on Intimate Inequalities, Ruptures and Dissonances*, **Sociological Research Online** | 已確認為 CC BY 4.0 開放取用、約 12,000–15,000 字，但 SAGE 與 MMU 機構典藏（e-space / repository）皆擋抓取，**僅取得摘要層級資訊**，未讀到兩個案例研究的實際內容 |

若你想要其中任何一篇，選項 4（補連結後重評）——你若手上有可讀入口或 PDF，我可以把它與現有三篇一同重評。Twamley 那篇的 CC BY 授權已確認，取得入口後即可作為主選候選。

---

## 互動選項

1. **確認主選** — AI 親密關係的公共論述（Frontiers in Sociology，sociology 首篇）
2. **改選備選 A** — 59 國單身率的社會與文化因素（純社會學、跨國計量）
3. **改選備選 B** — 34 個關係量表其實在測同一個東西（總分最高，但較複雜且屬 psychology）
4. **補連結後重評** — 提供入口或其他文章，與現有三篇一同評分
5. **重新搜尋** — 換主題方向
6. **本週跳過**

---

**狀態：AWAITING_CONFIRMATION。未收到上述明確確認語句前，不進入 ingest，不寫入 vault。**
