# Weekly Reading Ingest — MODES（strict / quick）

> 兩種 ingest 操作模式。預設 `config.modes.default = "strict"`。
> **核心安全閘門兩種模式皆相同**（見 `SAFETY.md`「Quick mode 下仍不可放寬的安全項」）。模式差異只在「產出物數量」與「lint / commit 時機」，不在安全。

## strict mode（重要文章、首次驗證、預設）

1. 候選報告 → 人工確認（三選一）
2. 產 **6 份 preview**：source-note / concept-note / project-link / review-card / weekly-log / safety-check（存 `config.paths.runsDir`/YYYY-Www/`config.paths.previewDirName`/）
3. preview 逐項審核
4. 正式寫入 vault
5. `npm run kb:index`
6. 告知並取得確認後跑 `npm run kb:lint`
7. lint 通過後 commit（只含本輪檔案）

## quick mode（忙碌週，但不犧牲安全）

仍要：
- 候選報告
- 人工確認（三選一）
- Free Access / domain / 不複製全文 三項檢查（不可略）
- `npm run kb:index`
- commit 前 `git status` 把關

可簡化：
- preview 從 6 份**合併為 1 份 summary preview**（涵蓋四類筆記要點 + safety check 結果）
- review card **允許 0 題**
- project-link 無明確關聯時**不產**
- `npm run kb:lint` **可延後**（例如月底批次跑），但 commit 前必須至少人工確認「無明顯 broken link / frontmatter 錯誤」
- 若 lint 延後，**必須在 weekly log 標記 `lint_status: deferred`**，待補跑後改為 `lint_status: passed`

quick mode **不是**無審核模式，**不得**變成自動 ingest——人工確認與安全閘門一律保留。

## 模式選擇

- 預設 strict。
- 使用者可在當週明確說「用 quick mode」切換。
- 不確定時用 strict。
- 首次處理某 domain、或文章特別重要時，建議 strict。
