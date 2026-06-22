# Weekly Reading Ingest（每週精讀策展器）

## 0. 目前狀態（accurate）

- **manual loop 已完成**並通過一次真實 ingest（首篇 commit `e0161bb`）：候選 → 確認 → preview → 寫入 → `kb:index` → `kb:lint` → commit。
- **Claude routine 自動觸發尚未真實測試**——至今全為手動執行。
- **暫不建議立刻掛 routine**；建議先手動跑 2–3 週確認會持續使用，並完成路徑可遷移性與穩定性修復後再開。
- 任何文件都不得把 routine 寫成「已完成」。

## 1. 產品定位

私人用 Claude routine + Obsidian 精讀策展工作流。每週由 Claude routine 搜尋高品質文章/論文，產出 1 主選 + 2 備選候選報告，在 Claude 界面等待使用者確認；確認後才把主選轉成 Obsidian 可吸收的知識筆記（source / concept / project-link / review-card）。

## 2. 非目標

- 不做 App / Web 產品化
- 不做多使用者
- 不做 Notion / Google Drive 整合
- 不做本地 OS 排程器（cron / launchd / Windows Task Scheduler）
- 不做自動 commit / push

## 3. 兩階段 Workflow

- **`weekly-reading-curate`**：讀取 config 與 vault context，搜尋候選、評分、判斷主選，產出候選報告。**不寫 vault**。
- **`weekly-reading-ingest`**：只在收到明確確認語句後，才把確認對象寫入 Obsidian vault。

## 4. 確認語句

只有以下三種會觸發 ingest，其他語句（包含「看看」「可以嗎」「先放著」「之後再說」）都不算確認：

- 確認主選
- 改選備選 A
- 改選備選 B

## 5. 寫入紅線

- 不改 `meta/index.md`
- 不改 `meta/log.md`
- 不改 `meta/lint.md`
- 不改 `tools/kb/*.mjs`
- 不寫 `raw/sources/french/`
- 不在 `wiki/projects/<project>/` 新增檔
- 不把候選報告寫進 vault

## 6. Domain / Source Folder 規則

- concept domain 只允許 `weekly-reading.config.json` 的 `allowedConceptDomains`：`ai-engineering / ai-workflow / design / finance / french`
- source folder 只允許 `allowedSourceFolders`：`articles / papers / videos / books`
- 法文來源按內容型態進 `raw/sources/articles/` 或 `raw/sources/papers/`，**不進 `raw/sources/french/`**（該資料夾為既有特殊資料區，v0 不自動寫入，也不修改 `tools/kb/new-source.mjs` 來支援它）

## 7. Routine 語意

- Claude routine（`routine.provider: "claude"`）每週六 10:00（Asia/Taipei）搜尋候選，這是 routine 行為，**不是本地 OS 排程器**。
- `localScheduler.enabled` 固定 `false`：不建立任何本機排程器。
- 手機備忘錄 / 提醒事項只提醒使用者去 Claude 確認本週主選，不是系統依賴，不連 Obsidian、不觸發任何寫入。

## 8. 資料夾與文件

```
weekly-reading.config.json           ← 唯一保留實際路徑（vaultRoot）之處；其餘文件不散落絕對路徑
README.md
routine-design.md                    ← Claude routine 使用設計（含 routine 未實測標示）
SAFETY.md                            ← 寫入範圍、紅線、Safety Checklist（由 ingest SKILL 引用）
FAILURE-HANDLING.md                  ← 全部失敗情境（由兩個 SKILL 引用）
MODES.md                             ← strict / quick 模式
.gitignore
runs/                                ← 候選報告與 preview 暫存（config.paths.runsDir）
  dry-run-001/                       ← v0 fixture，保留進 git
  real-curate-001/                   ← v0 首篇 fixture，保留進 git
.claude/skills/weekly-reading-curate/SKILL.md
.claude/skills/weekly-reading-ingest/SKILL.md
```

- 路徑去硬編碼：實際 Windows 路徑只放在 `config.vaultRoot`；文件改用相對概念（工具專案根目錄 = `toolRoot`、`config.paths.runsDir`、`config.paths.previewDirName`）。Mac 遷移時只需改 `config.vaultRoot`。
- skill 放在本工具專案內，不放進 vault 的 `.claude/skills/`，避免污染既有 KB skills（`kb-source-intake`、`kb-ingest` 等）。

## 9. strict / quick 模式

見 [`MODES.md`](MODES.md)。預設 strict（6 份 preview + 即時 lint + commit）；忙碌週可用 quick（合併 1 份 preview、review card 允許 0 題、lint 可延後並在 log 標 `lint_status: deferred`）。**兩模式的人工確認與安全閘門完全相同**，quick 不是無審核模式。

## 10. processed 策略

weekly-reading source 若同輪已產出至少一篇 concept note 且 output notes / weekly log 完成，依 `config.processedPolicy` 標 `processed: true`（concept note 內須含該 source 的 wikilink 以通過 lint），避免 `needs_review` 線性累積。首篇已套用。
