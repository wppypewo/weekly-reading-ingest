# 2026-W31 Safety Check + Depth Check

產出日期：2026-07-31
模式：strict
對象：Joel et al. (2020), PNAS 117(32): 19061–19071

---

## A. Safety Checklist（依 `SAFETY.md`）

| # | 檢查項 | 結果 | 說明 |
|---|---|---|---|
| 1 | 確認語句屬於三選一 | ⚠️ **通過（已聲明）** | 使用者輸入「確認 更新」。非字面上的「確認主選」，但緊接在編號選項 1 為「確認主選」的提問之後，且「更新」對應 `wiki/concepts/README.md` 的批准。已於回覆中明確聲明此解讀並請使用者更正 |
| 2 | 對應週候選內容存在 | ✅ | `runs/2026-W31/candidates-v3.md` |
| 3 | 候選報告含評分與主選理由 | ✅ | 五軸評分 + 勝出理由 + 深度可行性 |
| 4 | 改選備選低分警示 | — | N/A（確認主選，非改選） |
| 5 | Free Access = Yes 或有免費替代版 | ✅ | PNAS 官網 403，但 PMC7431040 提供免費全文，已實讀。免費替代版來源已寫入 source note |
| 6 | Main Pick 軟門檻 | ✅ | SQ 5 ≥ 3／RV 4 ≥ 3／Free Access Yes／domain 合法 |
| 7 | concept domain ∈ allowedConceptDomains | ✅ | `psychology`（2026-07-31 新增） |
| 8 | 二次確認（DOMAIN_DECISION） | — | N/A（未觸發） |
| 9 | source 寫入範圍限 `raw/sources/{articles,papers,videos,books}` | ✅ | `raw/sources/papers/` |
| 10 | 寫入範圍限 SAFETY.md 五類路徑 | ✅ | 見下方「預定寫入清單」 |
| 11 | project-link / review-card frontmatter 正確 | ✅ | review-card 為 `type: output` + `output_kind: review-card`；project-link 本週未產 |
| 12 | source 正文不改寫；備選只存標題/連結/理由/評分 | ✅ | source note 只放 3 段短節錄 + 繁中重寫摘要；備選只在 weekly log 記錄 |
| 13 | 不改 `meta/index.md`、`meta/log.md`、`meta/lint.md` | ✅ | 只追加 `meta/weekly-reading/log.md`（與 `meta/log.md` 為不同檔） |
| 14 | 不改 `tools/kb/*.mjs`、不動 `wiki/projects/` | ✅ | 未觸碰 |
| 15 | commit 前 `git status` 把關 | ⏸ | 待寫入後執行 |
| 16 | 候選報告不複製進 vault | ✅ | candidates v1/v2/v3 全部留在工具專案 `runs/` |
| 17 | 不 commit、不 push | ⏸ | 待使用者明確指示 |

### 不複製全文檢查（單獨標記）

source note 僅含 **3 段英文短引文**（各 1–2 句，作為引用線索）＋ 繁中重寫摘要。無整段複製，無全文轉載。✅

---

## B. Depth Check（依 2026-07-31 新增的 concept note 深度規格）

| 檢查項 | 實測值 | 結果 |
|---|---|---|
> 2026-07-31 更新：深度規格原為四條，第四條「必含 `## 我的辨證`」經使用者指示取消，現為三條。
> 本表已依三條規格重算。

| 檢查項 | 實測值 | 結果 |
|---|---|---|
| concept note 字數（`wc -m`，不含 frontmatter） | **10,082** | — |
| source note 字數（同上） | **4,716** | — |
| concept ≥ source | 10,082 > 4,716 | ✅ |
| ≥ 8,000 字下限 | 10,082 ≥ 8,000 | ✅ |
| 補入的原始文獻 | 無 | ✅ 來源自身厚度足夠（11 頁 PNAS + 補充材料），未動用回溯機制 |
| 章節覆蓋 | 見下 | ✅ |

### 章節覆蓋逐項

| 章節 | 狀態 |
|---|---|
| 核心結論 | ✅ 已填 |
| 背後原因 / 機制 | ✅ 已填——逐一展開四項主要論證 + 作者四項理論約束 + 中介解釋 + 與既有文獻關係 + 應用意涵，保留全部原始數值 |
| 使用場景 | ✅ 已填（4 項） |
| 容易混淆 / 常見陷阱 | ✅ 已填（7 項） |
| 與我目前專案 / 投資 / 學習的關係 | ✅ 已填（記明本週無專案連結） |
| 來源 | ✅ 已填 |
| 未確認 / 待查證 | ✅ 已填（4 項） |
| 相關概念 | ✅ 已填（2 條 wikilink） |

### 覆蓋要求逐項

| 要求 | 結果 |
|---|---|
| 逐一展開來源每個主要論證 | ✅ 四項論證各自成節 |
| 保留關鍵數據原始數值 | ✅ 兩張排序表（各 10 項含成功率）、四組變異量對照表、<5% 變化解釋力 |
| 寫出來源自陳限制與反論 | ✅ 五項限制全列 |
| 標注證據等級 | ✅ 同行評審 + 43 資料集整合分析；`confidence: high` |
| 二手轉述數據標注 | — N/A（全部為一手論文數據） |

---

## C. 結論

**Safety Check：通過**（第 1 項附解讀聲明）。
**Depth Check：通過**（三條規格全過）。

兩項閘門皆已通過，但**仍未寫入 vault**——尚有下方「待你裁示」三項未決。取得裁示後才執行寫入。

---

## D. 預定寫入清單（待 DEPTH_CHECK 通過後執行）

| # | 路徑 | 動作 |
|---|---|---|
| 1 | `raw/sources/papers/2026-W31-relationship-quality-predictability.md` | 新增 |
| 2 | `wiki/concepts/psychology/relationship-quality-predictability-limits.md` | 新增（`wiki/concepts/psychology/` 目錄一併建立） |
| 3 | `wiki/outputs/weekly-reading/review-cards/2026-W31-relationship-quality-predictability.md` | 新增 |
| 4 | `meta/weekly-reading/log.md` | 追加 W31 條目（不改既有內容） |
| 5 | `wiki/concepts/README.md` | 新增 `psychology` 條目（**已獲使用者批准**）。`sociology` 依 vault 2026-06-28「不預先建立空白領域資料夾」決策，本輪**不加**——待實際產出第一篇 sociology 筆記時再加 |

`wiki/projects/` 不動。`meta/index.md`、`meta/lint.md`、`tools/kb/*.mjs` 不動。

### 待你裁示

1. **project-link 本週不產**——五個專案皆為技術性，與本篇無實質關聯，依「不硬連」規定不產。strict mode 原定 6 份 preview，本輪為 5 份。請確認可接受。
2. **`wiki/concepts/README.md` 只加 `psychology` 不加 `sociology`**——理由如上表第 5 項。若你要兩個一起加，請明說。
3. `meta/weekly-reading/log.md` 檔頭殘留 Windows 路徑（見 weekly-log preview 末段），不在本次批准範圍，未改。
