# Weekly Reading Ingest — SAFETY

> 從 `weekly-reading-ingest/SKILL.md` 抽出的安全規則與寫入前 checklist，集中於此維護，避免主 skill 文件膨脹。
> **執行 ingest 前必讀本檔。** 路徑一律以 `weekly-reading.config.json` 為準（`vaultRoot`、`allowedConceptDomains`、`allowedSourceFolders`、`paths`），不在文件中散落絕對路徑。

## 寫入範圍（只允許這些路徑）

```
raw/sources/<allowedSourceFolders 之一>/        ← articles | papers | videos | books（不含 french）
wiki/concepts/<allowedConceptDomains 之一>/        ← concept 與 project-link（YYYY-Www-<slug>.md）都放這裡
meta/weekly-reading/log.md
```

所有路徑相對於 `config.vaultRoot`。若 `meta/weekly-reading/` 尚不存在，建立前須先取得使用者確認。

## 寫入紅線（永不觸碰）

- 不改 `meta/index.md`（只由 `npm run kb:index` 更新）
- 不改 `meta/lint.md`（只由 `npm run kb:lint` 更新）
- 不改 `meta/log.md`
- 不改 `~/ClaudeCode/projects/kb-tools/*.mjs`（含不為支援 french 而修改 `new-source.mjs`）
- 不寫 `raw/sources/french/`（既有特殊資料區）
- 不在 `wiki/projects/<project>/` 新增或修改檔（project-link 一律放對應的 `wiki/concepts/<domain>/`）
- 不把候選報告（`candidates.md`）寫進 vault
- 不把文章全文複製進 vault（source note 只存短節錄 + 繁中重寫摘要）
- 不自動 commit、不自動 push

## Safety Checklist（寫入前必逐項核對）

```
[ ] 確認語句屬於 {確認主選, 改選備選 A, 改選備選 B} 之一
[ ] 對應週候選內容存在（config.paths.runsDir 下 YYYY-Www/candidates.md，或當次對話中的候選報告）
[ ] 候選報告含評分與主選理由
[ ] 若為改選備選且觸發低分警示，已向使用者顯示警示文字（見 SKILL.md「低分備選改選警示」）
[ ] 被選中的文章 / 論文 Free Access 必須為 Yes，或有明確免費替代版（arXiv / 作者 PDF / 官方開放版）
      若 Free Access 為 No 或 Unclear → 停止 ingest，回報原因，不寫 vault（FREE_ACCESS_CHECK，無三選一補救）
[ ] Main Pick 軟門檻：Source Quality ≥ 3、Relevance ≥ 3、Free Access = Yes、domain ∈ allowedConceptDomains
      未滿足者不得自動為 Main Pick；若被選仍須符合本門檻或標「需要人工決策」
[ ] concept domain ∈ allowedConceptDomains
      若不屬於 → 進入 DOMAIN_DECISION，停止寫入，等待二次確認
[ ] 二次確認（僅當觸發 DOMAIN_DECISION 時才檢查）：
      已取得 {指定既有 domain / 批准本次不產 concept note / 取消 ingest} 三者之一
      未取得 → 不寫 source/project-link/review-card/log，整批中止
[ ] source 寫入範圍僅限 raw/sources/<articles|papers|videos|books>/（不含 french）
[ ] 寫入範圍僅限本檔「寫入範圍」列出的五類路徑
[ ] project-link frontmatter：type: output + output_kind 正確（review card 已停產，不再產出）
[ ] source 正文不改寫；備選只存標題/連結/理由/評分
[ ] 不改 meta/index.md、meta/log.md、meta/lint.md；不改 ~/ClaudeCode/projects/kb-tools/*.mjs；不動 wiki/projects/
[ ] commit 前已執行 git status，確認工作區只有本輪 weekly-reading 相關變更（見 FAILURE-HANDLING.md 第 7 項）
[ ] 候選報告留在 runs/ 或僅存於對話中，不複製進 vault
[ ] 不 commit、不 push（commit 由使用者明確指示後才做，且只含本輪檔案）
```

## Quick mode 下仍不可放寬的安全項

即使 quick mode（見 `MODES.md`），下列檢查一項都不能略過：

- 人工確認語句（三選一）
- Free Access 檢查
- domain 檢查（DOMAIN_DECISION）
- 不複製全文
- 不寫紅線路徑
- commit 前 git status 把關

quick mode 簡化的只是「產出物數量與 lint 時機」，不是安全閘門。
