# 2026-W29 每週精讀候選報告

產出日期：2026-07-18
模式：strict（預設）
狀態：AWAITING_CONFIRMATION

---

## 本週主題判斷

- **預設主題**：agent skill 的評估效度——skill 移植、生成與執行環境如何影響結果。
- **選題理由**：使用者的 skill-portability 實驗於 2026-07-18 完結，核心假說為「內容層可移植，執行層綁定 Claude harness 訓練」。本週搜尋刻意鎖定學術上與此對應的研究，讓個人實驗發現能連到正式文獻。
- **是否使用手動連結**：否，全部為自動搜尋。
- **是否含當週熱門內容**：主選為 2026-07-05 投稿的新論文，屬當月新內容。
- **候選同質性聲明**：三篇候選同屬 ai-engineering 且主題相近，本週未能在其他 domain 找到合格候選（見「風險與限制」）。

---

## Main Pick

| 欄位 | 內容 |
|---|---|
| Title | Measuring Harness-Induced Belief Divergence in Multi-Step LLM Agents |
| Author | Haiwen Yi, Xinyuan Song |
| Source | arXiv（preprint，未見同行評審紀錄） |
| URL | https://arxiv.org/abs/2607.04528 |
| Language | English |
| Estimated Reading Time | 約 90–120 分鐘（28 頁，含多張表格） |
| Type | paper |
| Free Access | **Yes**（PDF / HTML / TeX 皆開放；本次以 arXiv HTML 版讀取全文） |
| Topic | agent 評估效度、harness 設計、belief divergence |
| Domain | ai-engineering ✓（在 allowedConceptDomains 內） |
| Code | https://github.com/Hik289/Harness-induce-bias.git |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | arXiv preprint，兩位作者，無明確機構背書，未見同行評審 |
| Idea Density | 5 | 六種 harness 配置、belief 分解為 arrival/growth 兩成分、三個 benchmark 家族、BIWM 對齊協議，表格數據具體 |
| Long-term Value | 4 | 「harness 是實驗變數而非實作細節」這個框架有持久價值；具體指標可能被後續工作取代 |
| Relevance | 5 | 直接對應 skill-portability 實驗的核心假說 |
| Obsidian Fit | 5 | 可與既有 `llm-judge-self-inconsistency` 組成「評估效度」概念群 |

### 全文要點（已實讀 HTML 全文）

**設定**：固定基礎 LLM，三個 benchmark 家族——HIBench-Code（8 個受控編碼任務）、SWE-bench Verified、Terminal-Bench；受控研究用相同隨機種子。六種 harness：H₀ 原始參照／H₁ 結構化／H₂ 風險閘門／H₃ 重修復／H₄ 選擇性驗證／H₅ 成本感知。

**數據**：
- HIBench-Code 在 K=5 時，整體 belief divergence 落在 0.402–0.479；其中 arrival divergence（介面效應）逼近 1.0，growth divergence 只有 0.147–0.257 → **多數分歧來自即時介面變化，而非長程信念演化**。
- K=5 到 K=20 整體分歧不再系統性上升，但數值預測持續變動（K=1 的 0.044 升到 K=16 的 0.136）。
- SWE-bench Verified 上，風險閘門使失敗歸因分歧從 K=3 的 0.400 升到 K=5 的 0.800。
- BIWM 全套 instrumentation 使 growth divergence 增加 0.087–0.226；repair-unrolled logging 單項影響最大（重修復 harness 增加 0.195）。

**作者自陳的限制**：受控實驗規模刻意小（優先機制歸因而非覆蓋率）；公開 benchmark 數值不應解讀為整體效能估計；只能建立相關不能建立因果；結果依賴其自定的八欄位 belief schema。

---

## Backup A

| 欄位 | 內容 |
|---|---|
| Title | Agent Skill Evaluation and Evolution: Frameworks and Benchmarks |
| Author | Kexin Ding, Yang Zhou, Can Jin, Feng Tong, Mu Zhou, Dimitris N. Metaxas |
| Source | arXiv（survey，2026-06-09 投稿） |
| URL | https://arxiv.org/abs/2606.11435 |
| Language | English |
| Estimated Reading Time | 約 60–90 分鐘 |
| Type | paper（survey） |
| Free Access | **Yes** |
| Topic | agent skill 演化範式與 benchmark 分類 |
| Domain | ai-engineering ✓ |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 4 | 六位作者，含 Metaxas（Rutgers，資深學者） |
| Idea Density | 3 | survey 性質，分類清楚但深度不如實證研究 |
| Long-term Value | 4 | 作為 skill 生態的導航圖實用 |
| Relevance | 4 | 與 vault 的 KB skills 體系、skill-portability 實驗相關 |
| Obsidian Fit | 4 | 易沉澱成分類型 concept；但 survey 內容比實證更快過時 |

### 推薦理由

把「skill 評估」整個領域畫成地圖：四種演化範式（執行回饋／軌跡蒸餾／壓縮增補／強化學習）、六類 benchmark（效用／生成／檢索路由／安全稽核／軟體工程／真實環境）。指出三個結構性缺口：**無任何 benchmark 做縱向多輪演化評估**；指標多為二元通過／失敗，忽略 token 成本、延遲、錯誤型態；覆蓋不均（效用與安全跨 11 個專業領域，生成類只涵蓋 15 個子領域 20 個核心任務）。

---

## Backup B

| 欄位 | 內容 |
|---|---|
| Title | SkillGenBench: Benchmarking Skill Generation Pipelines for LLM Agents |
| Author | Yifan Zhou, Zhentao Zhang, Ziming Cheng 等 11 人 |
| Source | arXiv（2026-05-18 投稿） |
| URL | https://arxiv.org/abs/2605.18693 |
| Language | English |
| Estimated Reading Time | 約 60–90 分鐘 |
| Type | paper |
| Free Access | **Yes** |
| Topic | 自動生成 skill 的品質 benchmark |
| Domain | ai-engineering ✓ |

### 評分

| 項目 | 分數 | 理由 |
|---|---|---|
| Source Quality | 3 | arXiv preprint，作者機構不明確 |
| Idea Density | 4 | 187 任務、6 個 backbone、5 種生成方法、失敗模式有百分比拆解 |
| Long-term Value | 3 | benchmark 數字會隨模型迭代快速過時 |
| Relevance | 3 | 談自動生成 skill，而使用者是手寫 skill，關聯較間接 |
| Obsidian Fit | 3 | 可沉澱，但與現有 concept 群連結較弱 |

### 推薦理由

最值得注意的單一發現：**生成的 skill 並非普遍有益，有時表現比不給 skill 還差**。Pass@3 在 repository-grounded 任務只有 10.8–14.4%，document-grounded 為 21.4–25.0%。失敗模式拆解具體——repo 類以執行期／相依性問題為主（53%），程式文件類集中在介面／schema 精確度（85%），領域知識文件類則是狀態規則錯誤（44%）與數值公式錯誤（37%）。

---

## 主選勝出理由

**為何是主選**：它是唯一一篇把「執行環境本身作為變數」拿來量化的研究。skill-portability 實驗的核心假說是執行層綁定 Claude harness，這篇則證明——即使模型與任務固定，單是 harness 中介方式不同，agent 的內部信念就會顯著分歧，且**主要分歧來自即時介面差異而非長程累積**。這對該實驗「執行層未崩塌、只呈邊緣侵蝕」的觀察提供了一個可對照的機制解釋。

**為何勝過 Backup A**：A 是 survey，給的是地圖不是機制；本週的知識缺口不是「有哪些評估方法」，而是「執行環境如何改變結果」。

**為何勝過 Backup B**：B 談的是自動生成 skill 的品質，而使用者的 skill 是手寫的，關聯較間接。

**補的知識缺口**：vault 現有 `llm-judge-self-inconsistency` 處理的是「評分者不穩定」，本篇處理的是「執行環境不中立」。兩者合起來才構成完整的評估效度圖像——目前 vault 只有前半。

**適合沉澱的概念**：harness 作為實驗變數；belief divergence 的 arrival/growth 分解。

---

## 風險與限制

1. **主選是 preprint，未經同行評審**，Source Quality 只給 3。數據引用時須標明來源狀態。
2. **主選結果依賴作者自定的八欄位 belief schema**（作者自陳），換一套表徵可能得到不同分解。
3. **主選只能建立相關、無法建立因果**（作者自陳）：belief 分歧與後續行動改變是相關關係。
4. **與 skill-portability 實驗的對應是概念層呼應，不是同一件事**——該實驗測的是 skill 內容跨平台移植的效益衰減，論文測的是 harness 中介如何改變 agent 內部信念。沉澱概念時**不得**寫成「本論文驗證了我的實驗結論」。
5. **本週三篇候選同質**：都在 agent skill 評估這條線上。design domain 在 vault 中為 0 篇且 fashion-archive 剛完工，本應是明顯缺口，但本輪搜尋只找到 SEO 內容農場等級的「2026 設計趨勢」列表文，不符品質門檻，故不硬湊。

---

## 建議產生的 concept note（標題草案）

- `wiki/concepts/ai-engineering/harness-induced-belief-divergence.md`
  （或中文標題：「評估 harness 作為實驗變數」）

---

## 可能的 project link

`wiki/projects/skill-portability/` — 存在真實關聯（該專案核心假說即執行層綁定 harness），但**專案已於 2026-07-18 完結**，此連結屬回溯性補充，非後續開發依據。是否建立由使用者決定。

---

## 互動選項

1. 確認主選
2. 改選備選 A
3. 改選備選 B
4. 補連結後重評
5. 重新搜尋
6. 本週跳過
