> **PREVIEW — 尚未寫入 vault**
> 目標路徑：`meta/weekly-reading/log.md`
> **寫入方式：在既有 `## 2026-W31` 段落末尾「追加」以下內容，不修改該段落既有的任何一行**（第一篇 Joel et al. 的紀錄原樣保留）。

---

### 本週第二篇（2026-08-01 使用者指定精讀）

- Main pick: Characterizing the spiral: potential mechanisms in AI-associated delusions — Marc Augustin, Thomas A. Pollak, Hamilton Morrin — https://www.nature.com/articles/s44277-026-00065-0
- Backup A / Backup B: **無**。本輪文章由使用者直接指定，跳過搜尋階段，依 `FAILURE-HANDLING.md` A 區「只有 1 篇達標」的降級報告格式處理（成因不同：非搜不到，是已指定）
- Selected: main
- Scores（main）: Source Quality 4/5 / Idea Density 4/5 / Long-term Value 3/5 / Relevance 5/5 / Obsidian Fit 5/5（總分 21）
- 選擇理由：vault 既有的 AI 相關筆記全在處理 AI 系統本身的可靠性（評分者不穩、執行環境不中立），沒有一篇處理「AI 對使用者認知的作用」，本篇補的是缺的那一半。Long-term Value 僅 3——快速演變領域中的假說性框架，作者自陳需前瞻驗證，保值的是「三機制」這個拆解方式而非其結論。已符合軟門檻（SQ ≥ 3、Relevance ≥ 3、Free Access Yes、domain 合法）
- Domain 裁決：**psychology**（ai-engineering 亦成立；主體為精神病理機制，AI 為變因非主題，且避免 psychology 停在 1 篇。concept note 內以 wikilink 接向 ai-engineering 既有兩篇）
- Note paths：
  - source: [[raw/sources/papers/2026-W31-ai-associated-delusions]]
  - concept: [[wiki/concepts/psychology/ai-associated-delusions-amplification-spiral]]
  - project-link: **本週未產**（五個專案皆為技術性專案，無實質關聯，依規定不硬連）
  - review-card: [[wiki/outputs/weekly-reading/review-cards/2026-W31-ai-associated-delusions]]
- Review questions count：3
- 全文取得狀態：**已讀全文**（Nature 原網址回 303 導向 `idp.nature.com`，依 `FAILURE-HANDLING.md` A 區改走 redirect 入口重試成功）
- **本輪規格變更**：使用者於 2026-08-01 指示 concept note 字數下限由 **8,000 下修為 6,000**（「至少 6,000 字，寫不下可以更多」），本輪即適用。已同步修改 `.claude/` 與 `.agents/` 下的 curate／ingest 兩份 SKILL.md 共 4 檔，並在下限定義處加註「6,000 是下限不是目標」。**其餘深度規格未動**（不得短於 source note、必填章節與覆蓋要求、禁止灌水條款皆維持）
- **回溯文獻狀態**（narrative review 的必要配套，主論文幾乎全篇為二手轉述）：
  - ✅ Sharma et al., ICLR 2024（arXiv:2310.13548）——已回溯，取得具體數值（86%／98%／95%／<25% vs ~75% 等）
  - ✅ Moore et al.（arXiv:2603.16567）——已回溯，取得完整方法與數值（391,562 則訊息／4,761 對話／19 人／>80% 諂媚標記／33.3% 鼓勵暴力）
  - ⚠️ Dohnány et al., *Nature Mental Health* 4:336–345——**未回溯全文，僅依 abstract**。arXiv HTML v1/v2 皆 404，Oxford ORA 只顯示 abstract，本機無 PDF 解析工具（`pdftoppm` 未安裝）
  - ⚠️ Morrin et al., *Lancet Psychiatry* 13(6):522–530——**未回溯，付費牆**，KCL Pure 無 accepted version。此為本篇最核心的上游文獻且作者群重疊
  - ⚠️ Chandra et al.、Flathers et al.——**未定位**，相關內容全數依主論文轉述
  - 以上四項「未回溯／未定位」皆已在 concept note 的「來源」與「未確認 / 待查證」逐一標注
- Depth check（本輪實測，依下修後的 6,000 字下限）：concept **7,115 字** / source **3,121 字**；concept ≥ source ✅（差 3,994）；≥ 6,000 ✅；章節覆蓋 8/8 ✅
- Caveats：narrative（非系統性）review，納入範圍含**媒體報導**，證據等級極不均；多數個案缺乏診斷嚴謹度；**因果未建立**，不得寫成「AI 會導致妄想」；三機制**匯聚**本身仍是假說，未被實證展示；**0.07% 與換算出的約 50 萬人是 OpenAI 自行公布的內部估計**，判定標準未公開，不得當流行病學數據；Moore et al. 的 >80% 出自 19 人自選受害樣本，不是一般使用者比例，且部分編碼的 Cohen's kappa 低至 0.08；本篇 2026-06 發表，尚無足夠後續引用可判斷學界接受度。source/concept confidence 標 **medium**（低於第一篇的 high）
- 同週兩篇的關係：第一篇（Joel et al.）講自陳測量看不到關係的變化，本篇講 AI 順應會讓自陳的信念自我強化。一個是被動測不到，一個是主動被扭曲，形成對照而非重複
- Status：**preview 待審核**（尚未寫入 vault）
