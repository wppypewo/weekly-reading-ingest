# 2026-W32 Safety Check

執行日期：2026-08-09
模式：strict
狀態：待使用者審核 preview

## Safety Checklist（逐項核對）

| # | 檢查項 | 結果 | 依據 |
|---|---|---|---|
| 1 | 確認語句屬 {確認主選, 改選備選 A, 改選備選 B} | ✅ | 使用者輸入「確認主選」 |
| 2 | 對應週候選內容存在 | ✅ | `runs/2026-W32/candidates.md` |
| 3 | 候選報告含評分與主選理由 | ✅ | 三篇五軸評分齊備，含勝出理由與風險限制 |
| 4 | 改選備選低分警示 | 不適用 | 未改選 |
| 5 | Free Access = Yes 或有免費替代版 | ✅ | arXiv CC BY 4.0，HTML 全文已實讀 |
| 6 | Main Pick 軟門檻 | ✅ | SQ 3 ≥ 3、Relevance 5 ≥ 3、Free Access Yes、domain 合法 |
| 7 | concept domain ∈ allowedConceptDomains | ✅ | `ai-workflow` |
| 8 | DOMAIN_DECISION 二次確認 | 不適用 | 未觸發 |
| 9 | source 寫入範圍限 `raw/sources/<articles\|papers\|videos\|books>/` | ✅ | `raw/sources/papers/` |
| 10 | 寫入範圍限 SAFETY.md 列出的五類路徑 | ✅ | 見下方寫入清單 |
| 11 | project-link frontmatter 正確 | 不適用 | 本週未產 project-link |
| 12 | source 正文不改寫；備選只存標題/連結/理由/評分 | ✅ | source note 原文引述以短引呈現並標注原文；兩篇備選僅在 weekly log 記錄 |
| 13 | 不改 `meta/index.md`、`meta/log.md`、`meta/lint.md` | ✅ | 三檔皆不在寫入清單 |
| 14 | 不改 `tools/kb/*.mjs` | ✅ | 不在寫入清單 |
| 15 | 不動 `wiki/projects/` | ✅ | 不在寫入清單 |
| 16 | 候選報告不進 vault | ✅ | `candidates.md` 留在工具專案 `runs/` |
| 17 | 不複製全文進 vault | ✅ | source note 僅短引 6 處英文原句 + 繁中重寫摘要 + 數值表 |
| 18 | commit 前執行 `git status` | ⏳ | 待寫入後執行 |
| 19 | 不自動 commit、不 push | ✅ | commit 需使用者明確指示 |

## 預計寫入清單（3 檔）

| 動作 | 路徑 |
|---|---|
| 新增 | `raw/sources/papers/2026-W32-cli-coding-agents-microsoft-rollout.md` |
| 新增 | `wiki/concepts/ai-workflow/coding-agent-productivity-proxy-gap.md` |
| 追加 | `meta/weekly-reading/log.md`（檔尾新增 `## 2026-W32` 一節；frontmatter `updated` 改為 2026-08-09） |

檔名衝突檢查：三個目標路徑中，前兩者經確認不存在；第三者為既有檔案，僅追加不覆寫既有三節。

## DEPTH_CHECK 實測

| 檢查項 | 實測值 |
|---|---|
| concept 字數 | 7,208（`wc -m`，不含 frontmatter 與「## 相關概念」清單） |
| source 字數 | 4,522（`wc -m`，不含 frontmatter） |
| concept ≥ source | ✅ 成立 |
| 6,000 字下限 | ✅ 成立 |
| 章節覆蓋 | 8/8 — 核心結論 ✅／背後原因·機制 ✅／使用場景 ✅／容易混淆·常見陷阱 ✅／與我目前專案·投資·學習的關係 ✅／來源 ✅／未確認·待查證 ✅／相關概念 ✅ |
| 補入的原始文獻 | Agarwal et al. arXiv:2601.13597v2（已實讀方法／結果／限制章節，含完整 DiD 係數表）。主選自身 23 頁厚度足夠，此篇為對照加值 |

## 寫作規格檢查（2026-08-01 新增）

| 項目 | 上限 | 實測 |
|---|---|---|
| `——` 使用 | 全篇 ≤ 5 處 | 0 處 ✅ |
| 粗體 | 每節 ≤ 2 處 | 全篇 3 處（含 PREVIEW 標頭），最密集章節 1 處 ✅ |
| 路標語 | 禁止 | 未使用「值得注意的是」「這一點的意義在於」「必須同時記住的是」等 ✅ |
| 表格用途 | 僅多欄對照數據 | 4 張表全為數值對照（速度／品質／RQ1／RQ2）✅ |
| 全域禁用詞 | 禁止 | 已核對中英文清單，未出現 ✅ |
| 禁用句式 | 禁止 | 未出現「不僅是…更是…」「你不是…而是…」「從 X 到 Y」✅ |

## 未通過或需注意事項

無阻斷項。以下為需使用者知悉的內容層風險，已全數寫入 concept note 與 weekly log：

1. 主選為未經同行評審的預印本，confidence 標 `medium` 而非 `high`。
2. 作者利益關係明確（Microsoft 員工研究自家產品，RQ4 結論對自家有利），已在 concept note 獨立段落處理，並註明該數字不得單獨引用。
3. 三項未回溯項目（He et al. Cursor 研究、完整迴歸係數表、總樣本數）已在 concept note「未確認 / 待查證」逐一標注。

## 下一步

1. 使用者審核本 4 份 preview
2. 確認後正式寫入 3 檔
3. `npm run kb:index`
4. 告知後執行 `npm run kb:lint`
5. lint 通過 + `git status` 把關後，經明確指示才 commit
