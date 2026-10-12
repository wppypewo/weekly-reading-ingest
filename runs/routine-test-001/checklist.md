# routine-test-001：第一次雲端 routine 手動試跑檢查清單

> 狀態：**未執行**。建立日期 2026-10-12。
> 前提：`runs/2026-W42/routine-readiness-assessment.md` 的使用門檻（W42 起連續 3 週有回應）達標後才跑，最早 W44。
> 方式：建立 routine 時**不加排程 trigger**，只按 Run now 一次。routine 由使用者建立，Claude 不代為建立。
> 設定依據：`routine-design.md` 4.6。

## 建立前

- [ ] vault 本機沒有未推送的 commit（`git ls-remote origin HEAD` 與本機 `git rev-parse HEAD` 相同）
- [ ] 工具 repo 的最新文件已推到 GitHub master（routine 只讀得到遠端）
- [ ] Claude GitHub App 或 `/web-setup` 能存取兩個 private repo
- [ ] 環境：Network = Custom（含 4.6 清單，勾選 default list），setup script 裝 `poppler-utils`
- [ ] Connectors 全部移除
- [ ] prompt 使用 routine-design 4.2 草案，開頭加「先讀 `weekly-reading-ingest/.claude/skills/weekly-reading-curate/SKILL.md`」

## 試跑後逐項核對（打開 run 的 transcript，不看綠燈）

| # | 項目 | 怎麼確認 | 結果 |
|---|---|---|---|
| 1 | session 起始目錄與兩個 clone 的實際目錄名 | transcript 中 `pwd`、`ls` 的輸出 | |
| 2 | `CLAUDE_CODE_REMOTE` 為 `true` | transcript | |
| 3 | 讀到 vault，且報告寫出 vault HEAD commit 與日期 | 對照 `git ls-remote` | |
| 4 | `vaultRootRelative` 推測值正確，或靠同層 remote 比對找到 | transcript | |
| 5 | curate SKILL 有被讀取並照做（六項互動選項、五軸評分、Free Access 三值） | 報告內容 | |
| 6 | 學術站有沒有被 403 擋；WebSearch／WebFetch 是否受 allowlist 影響 | transcript、報告末尾的被擋網域 | |
| 7 | `pdftotext` 可用 | transcript | |
| 8 | 報告推到 `claude/weekly-reading-YYYY-Www`，該分支只多一個 `candidates.md` | `git ls-remote`、`git fetch` 後 `git diff master...<branch> --stat` | |
| 9 | 工具 repo master 未變 | `git ls-remote origin master` 對照試跑前 | |
| 10 | vault repo 沒有新分支、master 未變 | `git ls-remote` vault 全部 refs 對照試跑前 | |
| 11 | 沒有開 PR | GitHub | |
| 12 | 報告品質與手動 curate 相當（候選數、評分區分度、深度可行性欄位） | 人工比對最近一次手動報告 | |

## 試跑後決定

- 全部通過：`config.routine.tested` 改 `true`，再決定是否加排程 trigger、`config.routine.enabled` 改 `true`。
- 任一項失敗：記錄在本檔，修完再跑 routine-test-002，不加排程。
