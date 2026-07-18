# PREVIEW — safety check

日期：2026-07-18｜週次：2026-W29｜模式：strict

---

## Safety Checklist 逐項核對

| # | 檢查項 | 結果 | 說明 |
|---|---|---|---|
| 1 | 確認語句屬三選一 | ✅ | 使用者明說「確認主選」 |
| 2 | 對應週候選內容存在 | ✅ | `runs/2026-W29/candidates.md` |
| 3 | 候選報告含評分與主選理由 | ✅ | 五軸評分 + 勝出理由 + 風險限制齊備 |
| 4 | 低分備選改選警示 | N/A | 未改選備選 |
| 5 | Free Access = Yes | ✅ | arXiv 開放（PDF/HTML/TeX），已實際取得 HTML 全文 |
| 6 | Main Pick 軟門檻 | ✅ | SQ 3 ≥ 3、Relevance 5 ≥ 3、Free Access Yes、domain 合法。**SQ 剛好卡在門檻值，非高分過關** |
| 7 | concept domain ∈ allowed | ✅ | `ai-engineering` |
| 8 | DOMAIN_DECISION 二次確認 | N/A | domain 合法，未觸發 |
| 9 | source 寫入範圍 | ✅ | `raw/sources/papers/`（非 french） |
| 10 | 寫入範圍僅限五類路徑 | ✅ | 見下方寫入清單 |
| 11 | project-link / review-card frontmatter | ✅ | `type: output` + `output_kind` 正確 |
| 12 | source 正文不改寫；備選只存標題/連結/理由/評分 | ✅ | 備選 A/B 僅在 weekly log 記錄 |
| 13 | 不改 index / log / lint / tools；不動 wiki/projects/ | ✅ | 見下方「紅線確認」 |
| 14 | commit 前 git status | ⚠️ | **工作區有一項非本輪變更**，見下方 |
| 15 | 候選報告不複製進 vault | ✅ | 留在 `runs/2026-W29/` |
| 16 | 不自動 commit、不 push | ✅ | 等使用者明確指示 |

---

## 擬寫入清單（4 新增 + 1 追加）

| # | 路徑 | 動作 |
|---|---|---|
| 1 | `raw/sources/papers/2026-W29-harness-induced-belief-divergence.md` | 新增 |
| 2 | `wiki/concepts/ai-engineering/harness-induced-belief-divergence.md` | 新增 |
| 3 | `wiki/outputs/weekly-reading/project-links/2026-W29-harness-induced-belief-divergence.md` | 新增 |
| 4 | `wiki/outputs/weekly-reading/review-cards/2026-W29-harness-induced-belief-divergence.md` | 新增 |
| 5 | `meta/weekly-reading/log.md` | 追加一節 + 改 frontmatter `updated` |

檔名衝突檢查：以上四個新增路徑目前皆不存在，無覆寫風險。

---

## 紅線確認

- 不改 `meta/index.md`（將由 `npm run kb:index` 更新）✅
- 不改 `meta/lint.md`（將由 `npm run kb:lint` 更新）✅
- 不改 `meta/log.md`（與 `meta/weekly-reading/log.md` 是不同檔案，後者才是本輪目標）✅
- 不改 `tools/kb/*.mjs` ✅
- 不寫 `raw/sources/french/` ✅
- 不在 `wiki/projects/` 新增或修改檔 ✅（project-link 只以 wikilink **指向** `wiki/projects/skill-portability/`，不寫入該目錄）
- 不把 `candidates.md` 寫進 vault ✅
- 不把全文複製進 vault ✅（source note 只有一句節錄 + 繁中重寫摘要 + 數據摘錄）

---

## ⚠️ 第 14 項：工作區有非本輪變更

`git status` 顯示：

```
 M meta/source-queue.md
```

**這不是 weekly-reading 本輪產物**，是同一對話稍早依使用者指示更新的記載（推翻「vocabulary-bank warning 為預期」的舊敘述）。

依 `FAILURE-HANDLING.md` 第 7 項，處理方式為：**commit 時只 `git add` 逐一指定的本輪檔案，不得 `git add -A`**。

兩種可行做法，交由使用者決定：

- **(a)** 先單獨 commit `meta/source-queue.md`，再 commit 本輪 weekly-reading 五個檔案 → 兩個主題乾淨分離（建議）
- **(b)** 保留 `source-queue.md` 未提交，本輪只 commit weekly-reading 檔案 → 工作區留一項未提交變更

---

## 結論

第 1–13、15–16 項全部通過。第 14 項為已知情況且有明確處理方式，不構成 ABORT 條件。

**可以進入 WRITING 階段**（待使用者審核 preview 後）。
