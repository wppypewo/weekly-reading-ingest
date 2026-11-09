# 要不要現在掛 Claude routine：評估

> 2026-10-26 補註：本檔原放在 `runs/2026-W42/`，移到 `docs/`。文中的「README」指當時的規格 README，現為 [`SPEC.md`](SPEC.md)；行號是當時的版本。

日期：2026-10-12
範圍：只評估，不建立 routine、不改 config、不改規格文件。
依據：README §0 的三個前提（持續使用、路徑可遷移性、穩定性修復）、`runs/` 紀錄、vault `meta/weekly-reading/log.md`（唯讀）、Claude Code 官方文件 [Routines](https://code.claude.com/docs/en/routines) 與 [Desktop scheduled tasks](https://code.claude.com/docs/en/desktop-scheduled-tasks)（2026-10-12 讀取）。

## 結論

**現在不建議掛。** 三個前提中，持續使用只部分成立，路徑可遷移性只完成本機那一半，穩定性從未實測。最大的問題不在文件，而在 routine 的執行位置：現行規格假設 routine 能讀本機的 vault，但雲端 routine 是在新的 clone 裡執行，讀不到本機檔案；照現行 `FAILURE-HANDLING.md` C 區，它每週都會停在「vaultRoot 不可達」。

建議順序：先修文件與 config 的不一致，再決定執行位置（雲端或本機 Desktop 排程），然後只用 **Run now 手動試跑一次**，不排程。試跑結果與手動 curate 比對過，才談排程。

---

## 前提一：持續使用

### 實際紀錄

你的前提是「W31–W33、W38–W39 有跑」。實測還要加上 W26、W27、W29。W26 到 W41 共 16 週：

| 週 | 狀態 | 候選來源 |
|---|---|---|
| W26 | curate 兩次，ingest 一篇 | 搜尋 |
| W27 | curate，**未 ingest**（vault log 無 W27） | 搜尋 |
| W28 | 無紀錄 | — |
| W29 | curate + ingest | 搜尋 |
| W30 | 無紀錄 | — |
| W31 | curate 三版 + 第二篇，ingest 兩篇 | 搜尋 |
| W32 | curate + ingest | 搜尋 |
| W33 | curate + ingest | 搜尋（主題由你指定） |
| W34–W37 | 無紀錄（連續 4 週） | — |
| W38 | ingest | **你指定的文章，跳過搜尋** |
| W39 | ingest 兩篇 | **兩篇都是你指定，跳過搜尋** |
| W40–W41 | 無紀錄（2 週） | — |
| W42 | 本次 curate，待確認 | 搜尋 |

- 有活動的週：8 / 16。有 ingest 的週：7 / 16，共 9 篇。
- 最長中斷：W34–W37，連續 4 週。
- README 要求「手動跑 2–3 週確認會持續使用」。W31–W33 連續三週在 8 月達到過這個條件，但之後中斷了 4 週。

### 對 routine 的意義

routine 自動化的是**搜尋 curate** 這一段。這一段最後一次使用是 W33（2026-08-16），W38、W39 你都是自己帶文章來。換句話說，最近兩個有活動的週，routine 若有排程，它產的報告都不會被用到。

反方論點也要列出：中斷可能正是因為沒有東西每週提醒你。routine 每週六產一份報告擺在那裡，也許能減少中斷。現有資料無法分辨這兩種解釋。這是可以靠試跑回答的問題，不是靠推論。

**判定：部分成立。** 你會回來用，但用法已經從「讓 Claude 找」轉向「自己帶文章來」。掛 routine 前要先決定：你帶文章來的週，routine 的報告怎麼處理（直接忽略、或 routine 改成讀一個你丟文章的佇列）。

---

## 前提二：路徑可遷移性

### 已完成（本機）

- `weekly-reading.config.json` 的 `vaultRoot` 已在 W31 從 `D:/...` 改為 Mac 路徑。
- kb 腳本路徑已在 `0b68604`（2026-09-16）改指 `~/ClaudeCode/projects/kb-tools/`，README 第 40、50 行已更新。

### 未完成（文件殘留）

| 檔案 | 行 | 殘留內容 |
|---|---|---|
| `.claude/skills/weekly-reading-curate/SKILL.md` | 49 | 「不得改 `tools/kb/*.mjs`」，舊路徑 |
| `SAFETY.md` | 21、48 | 同上 |
| `README.md` | 81 | 「實際 Windows 路徑只放在 `config.vaultRoot`」 |
| `routine-design.md` | 98 | 「routine 無法存取本機 D 槽」 |

這四處不影響手動執行，但 routine 會照字面讀 SKILL 與 SAFETY。

### 未完成（雲端執行的路徑問題）

這一段是本評估最主要的發現。依官方文件：

- 雲端 routine「Access to local files: No (fresh clone)」。每次執行都從 GitHub clone 你選定的 repo。
- 可以選多個 repo，所以技術上可以同時 clone `weekly-reading-ingest` 和 vault（`ricky-knowledgebase`）。

但現行設計沒有為這種情況準備：

1. **`vaultRoot` 是 Mac 絕對路徑**（`/Users/ricky/ClaudeCode/KnowledgeBase/Ricky-KnowledgeBase`）。雲端 clone 的位置不同，config 沒有覆寫機制。照 `FAILURE-HANDLING.md` C 區第二列，routine 會「停止；回報 vaultRoot 不可達」，每週都一樣。
2. **雲端讀到的 vault 是舊的。** 2026-10-12 用 `git ls-remote` 實測：vault 本機 `053a842` 領先遠端 `19e4055`（2026-09-23）5 個 commit；`schema/context/current-focus.md` 另有未提交的修改（不是本次 session 改的）。雲端 routine 讀到的 current-focus 會停在三週前。要用雲端，vault 必須固定推送。
3. **候選報告存放規則與雲端行為不符。** SKILL 第 42 行與 routine-design 第 10 步假設「無法存取本機 → 報告只留在對話」。實際上雲端 routine 可以寫進 clone、推到 `claude/` 開頭的分支。要不要讓它推，規格沒決定。
4. **clone vault 等於給 routine vault 的寫入權。** 雲端 routine 沒有權限確認（文件原文：「there is no permission-mode picker」），「不寫 vault」只靠 prompt 約束。要靠 GitHub branch ruleset 擋，或乾脆不 clone vault、改由別的方式提供 context。

### 本機替代方案

官方文件另有 Desktop 本機排程（Desktop app → Routines → New routine → Local）：在你的 Mac 上執行，可以讀本機檔案，路徑問題全部消失；權限模式可逐項設定。限制是 app 要開著、電腦要醒著；睡過排程時間會略過，醒來後只補跑最近一次。

這和 README「不做本地 OS 排程器」的精神是否衝突，要你判斷：它不是 cron 或 launchd，但它是在本機跑。`config.localScheduler.enabled: false` 的原意也要一起確認。

**判定：本機成立，雲端不成立。**

---

## 前提三：穩定性

### routine 本身

- **從未實測。** `config.routine.tested: false`，README §0 與 routine-design 都這樣寫。
- **config 自相矛盾。** `routine.enabled: true` 與 `tested: false`、README「暫不建議立刻掛」同時存在。目前沒有實際 routine 存在，所以 `enabled: true` 沒有效果，但它和文件說法不一致。
- **routine 是 research preview。** 官方文件註明行為、限制、API 都可能變動。
- **綠燈不等於成功。** 官方文件：run 清單的綠色狀態只代表 session 沒有基礎設施錯誤；被擋的網路請求、任務層級的失敗都只在 transcript 裡。試跑後必須讀 transcript。
- **排程時間。** config 寫 10:00；官方文件說整點排程可能延遲數分鐘，建議改成 10:07 這類非整點。

### 抓取失敗紀錄（手動執行時發生，routine 也會碰到）

| 週 | 失敗 | 手動時怎麼解決 |
|---|---|---|
| W31 | Aeon 連續三次 HTTP 429 | 放棄該來源 |
| W31 | arXiv HTML 404、PDF 文字抽取失敗 | 只讀到摘要，不得列主選 |
| W31 | Nature 303 導向 `idp.nature.com`；PNAS 403 | 改走 redirect 入口、改讀 PMC |
| W33 | SAGE 全站 403 或回首頁 | 兩篇排除 |
| W38 | openai.com 對 curl 與 WebFetch 皆 403 | **改用內建瀏覽器**讀取成功 |
| W42 | WebFetch 讀 PDF 只拿到二進位內容 | **本機 `pdftotext`** 轉純文字 |

W38 與 W42 的解法都依賴本機工具。雲端 routine 有沒有內建瀏覽器、預設映像有沒有 `pdftotext`，**我沒有查到，標為未確認**；試跑時要特別檢查。

### 雲端網路限制

官方文件：Default 環境是 Trusted 網路，只放行套件庫、雲端 API 等預設清單，其他網域回 `403 host_not_allowed`。curate 要抓 Econometrica、arXiv、BFI、Frontiers、Nature 這類學術站，大多不在預設清單內。需要把環境改成 Custom（自己列網域）或 Full。WebFetch 工具的請求是否走這條受限網路，文件沒有寫明，**未確認**。

### 用量

routine 與互動 session 共用訂閱額度。本週這次 curate 抓了三篇全文、兩份 PDF 轉文字、多輪查證，是用量偏高的工作。每週六自動跑一次，即使你那週不看報告，額度也會被扣。

**判定：未成立。**

---

## 還缺什麼（依建議順序）

### 1. 文件與 config 修正（小改動，可以直接做）

- [x] SKILL.md 第 49 行、SAFETY.md 第 21、48 行：`tools/kb/*.mjs` 改為 `~/ClaudeCode/projects/kb-tools/*.mjs`
- [x] README.md 第 81 行：拿掉「Windows」
- [x] routine-design.md 第 98 行：「本機 D 槽」改為「本機檔案」
- [x] `config.routine.enabled` 改 `false`，直到試跑通過；排程時間改 10:07（SKILL description、README、routine-design 同步改）

2026-10-12 依使用者回覆「修文件殘留和 config」完成。

### 2. 需要你決定的事

- [x] **執行位置**：雲端 routine，或本機 Desktop 排程。我的建議是本機：現行規格（讀 vault、寫 `runs/`、`pdftotext`、內建瀏覽器備援）全部假設本機環境，改成雲端要動的地方多很多。代價是電腦要開著。→ 2026-10-12 使用者選**雲端**，適配項目見下一條。
- [x] **你帶文章來的週怎麼辦**：routine 照跑但你忽略報告，或 routine 先檢查有沒有你指定的文章。→ 2026-10-12 採建議：routine 照跑，在該次 run 回「補連結後重評」或「本週跳過」，不加偵測機制（routine-design 4.3）。
- [x] 若選雲端：vault 要不要讓 routine clone、推送頻率、`runs/` 要不要讓它推到 `claude/` 分支、要不要設 branch ruleset、網路要開 Custom 還是 Full。→ 2026-10-12 採建議：clone vault（只讀）、報告推 `claude/` 分支、網路 Custom。ruleset 不設：官方文件說 routine 用你的 GitHub 身分推送，ruleset 分不出你和 routine（routine-design 4.6）。

### 3. 使用的門檻（建議）

- [ ] 從 W42 起，連續 3 週有搜尋式 curate 並且你有回應（確認、改選、或跳過都算）。這是 README「手動跑 2–3 週」的重跑，因為上一次達標後中斷了 4 週。

### 4. 一次手動試跑（由你啟動，不排程）

- [ ] 在選定的執行位置建立 routine，但**不加排程**（雲端不加 trigger，本機選 Manual），按一次 Run now。
- [ ] 讀完整 transcript，不只看綠燈。檢查：有沒有讀到 current-focus、有沒有被網路擋、PDF 有沒有抽到文字、有沒有寫 vault 或推送任何東西。
- [ ] 把結果記在 `runs/routine-test-001/`，和同一週的手動 curate 比對。
- [ ] 通過後才把 `config.routine.tested` 改 `true`、加排程。

---

## 我查過但無法確認的部分

- 雲端 routine 的預設映像是否有 `pdftotext`、是否有瀏覽器工具。
- 雲端 routine 中 WebFetch 的請求是否受環境網路白名單限制。
- W34–W37、W40–W41 中斷的原因。`runs/` 與 vault log 都沒有記錄，我沒有推測。
