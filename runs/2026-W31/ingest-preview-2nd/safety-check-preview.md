> **PREVIEW — 尚未寫入 vault**
> 依 `SAFETY.md` 的 Safety Checklist 逐項核對。本檔為 W31 **第二篇**的檢查結果。

# Safety Check — 2026-W31 第二篇（AI-Associated Delusions）

## 狀態機路徑

```
AWAITING_CONFIRMATION
  └─ 使用者 2026-08-01「確認主選」 ✅
FREE_ACCESS_CHECK        → Yes（Nature Open Access，已讀全文） ✅
MAIN_PICK_THRESHOLD_CHECK → SQ 4≥3、RV 5≥3、Free Yes、domain 合法 ✅
DOMAIN_CHECK             → psychology ∈ allowedConceptDomains ✅（未觸發 DOMAIN_DECISION）
SAFETY_CHECK             → 見下表
WRITING                  → 5 份 preview 已產出（project-link 不產，理由見下）
DEPTH_CHECK              → 三項全過 ✅
INDEX / LINT / COMMIT    → **尚未執行**，等使用者審核 preview
```

## Safety Checklist 逐項

| # | 檢查項 | 結果 |
|---|---|---|
| 1 | 確認語句屬於三選一 | ✅ 「確認主選」（2026-08-01） |
| 2 | 對應週候選內容存在 | ✅ `runs/2026-W31/candidates-2nd-pick.md` |
| 3 | 候選報告含評分與主選理由 | ✅ 五軸評分 + 勝出理由 + 風險限制 |
| 4 | 低分備選改選警示 | — 不適用（未改選備選；本輪無備選） |
| 5 | Free Access = Yes 或有免費替代版 | ✅ Nature Open Access，直接全文 |
| 6 | Main Pick 軟門檻 | ✅ SQ 4／RV 5／Free Yes／domain 合法 |
| 7 | concept domain ∈ allowedConceptDomains | ✅ `psychology` |
| 8 | 二次確認（僅 DOMAIN_DECISION 時） | — 未觸發 |
| 9 | source 寫入範圍僅限 `raw/sources/<articles\|papers\|videos\|books>/` | ✅ `raw/sources/papers/` |
| 10 | 寫入範圍僅限 SAFETY.md 五類路徑 | ✅ 見下方「本輪寫入清單」 |
| 11 | project-link / review-card frontmatter 正確 | ✅ review-card 為 `type: output` + `output_kind: review-card`；project-link 本輪不產 |
| 12 | source 正文不改寫；備選只存標題/連結/理由/評分 | ✅ 原文僅短引定義句，其餘繁中重寫；本輪無備選 |
| 13 | 不改 `meta/index.md`、`meta/log.md`、`meta/lint.md`；不改 `tools/kb/*.mjs`；不動 `wiki/projects/` | ✅ 均未列入寫入清單 |
| 14 | commit 前已執行 `git status` | ⏳ **寫入前需重跑**。2026-08-01 產 preview 前實測：vault 工作區乾淨，HEAD `ec224a4` |
| 15 | 候選報告不複製進 vault | ✅ 留在 `runs/` |
| 16 | 不 commit、不 push | ✅ 尚未執行，待使用者指示 |

## 本輪寫入清單（審核通過後才執行）

| # | 路徑 | 動作 |
|---|---|---|
| 1 | `raw/sources/papers/2026-W31-ai-associated-delusions.md` | 新增 |
| 2 | `wiki/concepts/psychology/ai-associated-delusions-amplification-spiral.md` | 新增 |
| 3 | `wiki/outputs/weekly-reading/review-cards/2026-W31-ai-associated-delusions.md` | 新增 |
| 4 | `meta/weekly-reading/log.md` | **追加**於既有 `## 2026-W31` 段落末尾，不改動第一篇的任何一行 |

**檔名衝突檢查**：三個新增路徑均與 W31 第一篇（`2026-W31-relationship-quality-predictability`）不同名，無衝突。寫入前仍須實測確認檔案不存在。

**project-link 不產**：四個專案（movie-app / personal-website / portfolio-tracker / skill-portability）皆為技術性專案，與本篇無實質關聯。依 `FAILURE-HANDLING.md` D 區規定寫「本週沒有明確專案連結」，不硬連。故本輪為 **5 份 preview**（與第一篇一致，非 6 份）。

## DEPTH_CHECK 實測（依 2026-08-01 下修後的 6,000 字下限）

| 檢查項 | 實測 | 結果 |
|---|---|---|
| concept 字數（`wc -m`，扣 frontmatter 與末尾 wikilink 清單） | **7,115** | — |
| concept 字數（含「相關概念」段） | 7,598 | 參考值 |
| source 字數（`wc -m`，扣 frontmatter） | **3,121** | — |
| concept ≥ source | 7,115 ≥ 3,121（差 3,994） | ✅ |
| ≥ 6,000 字下限 | 7,115 ≥ 6,000 | ✅ |
| 章節覆蓋 | 核心結論 ✅／背後原因·機制 ✅／使用場景 ✅／容易混淆·常見陷阱 ✅／與專案關係 ✅／來源 ✅／未確認·待查證 ✅／相關概念 ✅ | **8/8 ✅** |
| 補入的原始文獻 | Sharma et al.（ICLR 2024, arXiv:2310.13548）、Moore et al.（arXiv:2603.16567）**已完整回溯**；Dohnány et al.、Morrin et al. 僅 abstract；Chandra et al.、Flathers et al. 未定位——四項皆已在 concept note 標注 | ✅ 已標注 |

**未灌水聲明**：7,115 字中的增量來自兩篇實際回溯的原始文獻（Sharma 的七項數值、Moore 的方法與十四項數值及四類螺旋），非複述主論文或堆疊形容詞。未回溯者一律標明，未以轉述充數。

## 規格變更紀錄（本輪一併執行）

使用者 2026-08-01 指示：concept note 字數下限由 8,000 下修為 **6,000**，「寫不下可以更多」，本次適用。

| 檔案 | 變更 |
|---|---|
| `.claude/skills/weekly-reading-ingest/SKILL.md` | 5 處 8,000 → 6,000；第 53 行加註「6,000 是下限不是目標——來源撐得起就寫更多，不得因剛過門檻而收尾。（2026-08-01 由 8,000 下修為 6,000。）」 |
| `.agents/skills/weekly-reading-ingest/SKILL.md` | 同上 |
| `.claude/skills/weekly-reading-curate/SKILL.md` | 3 處 8,000 → 6,000 |
| `.agents/skills/weekly-reading-curate/SKILL.md` | 同上 |

**未動的部分**：不得短於 source note、必填章節與覆蓋要求、薄來源處理與禁止灌水條款、`DEPTH_CHECK` 狀態機——全部維持原狀。`runs/` 下的歷史報告（v1/v2/v3 與第一篇 preview）保留原文，不回溯改寫。

## 尚未執行

- `npm run kb:index`
- `npm run kb:lint`（strict mode：需另行取得確認）
- `git add` / `git commit`（只加本輪逐一指定的檔案，不用 `git add -A`）
