# Weekly Reading Ingest

[English](README.md) | 繁體中文

每週精讀策展器：一組 Claude Code skill，每週找一篇值得精讀的文章或論文，等使用者確認後，才把它整理成 Obsidian 知識庫的筆記。

- **兩階段、中間必須有人確認。** `weekly-reading-curate` 搜尋並評分，產出 1 主選 + 2 備選的候選報告，不寫入知識庫。`weekly-reading-ingest` 只在收到「確認主選」「改選備選 A」「改選備選 B」三句話之一才動手；「看看」「可以嗎」「先放著」都不算確認。
- **寫入有紅線。** 不改知識庫的索引、log、lint 檔，不碰既有的特殊資料夾，不在專案資料夾新增檔案，候選報告永遠不進知識庫。完整清單在 [`SAFETY.md`](SAFETY.md)。
- **一次寫成一整組筆記。** 確認後產出 source、concept、project-link、複習卡、weekly log，先寫成 preview 給人看，通過安全檢查再寫入，然後跑知識庫的 index 與 lint。

私人工具，只給一個人用；沒有 App、沒有多使用者，也不做本機排程器。

## 目前狀態

- 手動流程已經完整跑通，並完成一次真實 ingest：候選 → 確認 → preview → 寫入 → index → lint → commit。
- 每週自動觸發（Claude 雲端 routine）**還沒實測**，設定裡維持 `routine.enabled: false`。試跑前的評估與檢查清單在 [`docs/`](docs/)。

## 一次完整的範例

[`runs/real-curate-001/`](runs/real-curate-001/) 是第一次真實執行留下的全部產物：

| 檔案 | 是什麼 |
|---|---|
| `candidates.md` | 候選報告：本週主題判斷、主選與兩個備選，每篇依來源品質、想法密度、長期價值、相關性、Obsidian 適配度五軸評分 |
| `ingest-preview/` | 確認主選後寫入前的 6 份 preview：source note、concept note、project-link、複習卡、weekly log、安全檢查 |
| `closeout.md` | 寫入、index、lint、commit 的結果 |

## 怎麼運作

| 檔案 | 內容 |
|---|---|
| [`.claude/skills/weekly-reading-curate/`](.claude/skills/weekly-reading-curate/SKILL.md) | 第一階段：讀設定與知識庫脈絡，搜尋、評分、產出候選報告 |
| [`.claude/skills/weekly-reading-ingest/`](.claude/skills/weekly-reading-ingest/SKILL.md) | 第二階段：收到確認語句後，產 preview、檢查、寫入 |
| [`weekly-reading.config.json`](weekly-reading.config.json) | 知識庫路徑、允許的 concept domain 與 source 資料夾、主選門檻、模式 |
| [`SAFETY.md`](SAFETY.md) | 寫入範圍、紅線、安全檢查清單 |
| [`FAILURE-HANDLING.md`](FAILURE-HANDLING.md) | 各種失敗情境怎麼停、怎麼回報 |
| [`MODES.md`](MODES.md) | strict（6 份 preview、即時 lint）與 quick（合併 preview、lint 可延後）；兩種的人工確認相同 |
| [`routine-design.md`](routine-design.md) | 每週自動觸發的設計（雲端 routine，未實測） |
| [`docs/SPEC.md`](docs/SPEC.md) | 完整規格：定位、非目標、確認語句、紅線、domain 規則、processed 策略、標題格式 |

在 Claude Code 裡開這個 repo，說「本週精讀」就會觸發第一階段。要真的寫入，得先把 `weekly-reading.config.json` 的 `vaultRoot` 指到自己的 Obsidian 知識庫；它假設知識庫裡已有 index、lint 的腳本與既定的資料夾結構，換成別的知識庫要先改設定與 `SAFETY.md`。

## 授權

[MIT](LICENSE)。`runs/` 範例裡摘要、引用的文章屬於各自的作者，報告只放連結與摘要。
