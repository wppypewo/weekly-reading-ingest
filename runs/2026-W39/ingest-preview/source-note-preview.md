> **PREVIEW** — 預計寫入 `raw/sources/videos/2026-W39-dario-amodei-end-of-exponential.md`
> 尚未寫入 vault。`raw/sources/videos/` 目錄目前不存在，寫入時新建。

---

---
type: source
status: raw
domain: ai-workflow
source: Dwarkesh Podcast（YouTube 影片與 dwarkesh.com 官方逐字稿，長篇訪談，未經審查）
author: Dwarkesh Patel（主持）、Dario Amodei（受訪）
published: 2026-02-13
created: 2026-09-21
updated: 2026-09-21
processed: true
related_concepts:
  - "[[wiki/concepts/ai-workflow/coding-automation-spectrum]]"
tags: []
---
# Dario Amodei — We are near the end of the exponential

## Source

- 影片：https://youtu.be/n1E9IZfvGMA
- 逐字稿：https://www.dwarkesh.com/p/dario-amodei-2
- 類型：podcast 長篇訪談，口語，無同行評審
- 發布：2026-02-13
- 篇幅：影片 2 小時 22 分；逐字稿約 22,300 英文字（2026-09-21 抓取 HTML 轉純文字實測）
- 受訪者身分：Anthropic 共同創辦人暨執行長。訪談中的營收、內部生產力、對競爭對手的評價都是當事人自述，無法查核
- 取用：逐字稿頁公開，HTTP 200，全文已實讀；本筆記只作摘要，引文限短句

## 原始摘錄 / 摘要

### 訪談結構

逐字稿依時間碼分七段。開頭談 scaling：Amodei 重述他 2017 年的「Big Blob of Compute」假說，認為強化學習（RL）和預訓練一樣呈 log-linear 成長。他把預訓練與 RL 放在「人類演化」和「個人一生的學習」之間，把 in-context learning 放在長期與短期學習之間。

第二段（12:36）Dwarkesh 問為什麼是一年而不是十年。Amodei 說十年內出現「數據中心裡的天才國度」他有 90% 把握，剩下的不確定性來自台海、晶圓廠等外部事件，以及無法驗證對錯的任務。他說 coding 這類可驗證任務「one or two years」就能端到端完成。接著兩人談「AI 寫了多少程式碼」該怎麼算，Amodei 列出一條自動化光譜（見下）。再來談擴散：Anthropic 營收 2023 年 0 到 1 億美元、2024 年到 10 億、2025 年到 90–100 億美元，2026 年 1 月又增加「another few billion」。他說有兩條快速的指數曲線，一條是模型能力，一條是模型進入經濟的擴散，後者受法務、資安、採購、組織內說服的拖慢。

第三段（29:42）談持續學習是否必要。Dwarkesh 以自己的影片剪輯師為例，說模型無法像員工一樣在幾個月內累積對偏好的理解。Amodei 說電腦操作是目前擋住部署的因素之一，OSWorld 從約 15% 升到 65–70%。生產力研究的交鋒在這一段（見下）。Amodei 說持續學習「a good chance」在一兩年內解決，較長的 context 是工程與推論問題。

後四段談算力與財務（46:20 起）、監管（01:31:19 起）、美中與 constitution（01:47:41 起）。Amodei 的論點包括：營收預測差一年就可能破產，所以不能照 AGI 將至的信念無限買算力；實驗室盈虧主要取決於需求預測的誤差；市場會是少數寡占；反對十年聯邦禁止州法，支持聯邦立標準後先占；民主國家要在制定規則時握有較強籌碼。本輪 concept note 不處理這四段。

### 自動化光譜（12:36 段）

Dwarkesh 問「幾乎到了」是用什麼指標。他說編譯器寫出了所有機器碼，行數和生產力提升是兩回事。Amodei 同意，說他八九個月前預測「三到六個月內 AI 會寫 90% 的程式碼」，這在 Anthropic 和部分下游使用者身上實現了，他自稱這是「a very weak criterion」，外界誤讀成「不需要 90% 的工程師」。他列出的光譜依序是：模型寫 90% 的程式碼；寫 100%；完成 90% 端到端軟體工程任務（編譯、架設叢集與環境、測試功能、寫備忘錄）；完成今天 100% 的軟體工程任務；軟體工程師需求減少 90%。他說第四階段發生時工程師仍有更高層的工作，第五階段他認為會發生，並提到在〈The Adolescence of Technology〉用農業做過同樣的光譜。

Dwarkesh 追問：即使在全新專案裡用 Claude Code，他也沒看到「renaissance of software」，也就是大量原本不會存在的新功能。

### 生產力研究的交鋒（29:42 段）

Dwarkesh 提到去年一項研究：資深開發者在熟悉的 repo 上工作，自覺變快，但他描述「看產出與合併回去的量」有 20% 的 downlift。逐字稿頁內連結指向 METR 2025-07-10 的研究。

Amodei 回應：在 Anthropic 內部這件事「really unambiguous」。公司承受龐大商業壓力，沒時間做自我感覺良好的事；會擔心競爭對手使用自家工具，正因為工具有用；每幾個月一次的模型發布就是最終產出。

Dwarkesh 反駁兩點：自覺變快本來就是這類研究預測會出現的現象；如果 coding 模型帶來巨大生產力，擁有最好 coding 模型的公司應該累積出持續領先，實際上三家實驗室每幾個月輪流領先。

Amodei 的回答是「雪球模型」：coding 模型現在大約帶來 15–20% 的全要素加速，六個月前約 5%，5% 感覺不出來。優勢會逐漸擴大，他給的示意序列是 10%、20%、25%、40%。他引用 Amdahl's law，說要把阻礙閉環的環節逐一移除。他也說其他公司會在內部使用 Anthropic 的模型，這讓領先不易拉開。

### 限制

- 口語來源，Amodei 多次自稱數字是示意（stylized）。15–20%、5% 沒有給出測量方式。
- 營收與內部生產力無第三方數據。
- 發布於 2026-02-13，早於 METR 自己在 2026-02-24 發布的後續更新，兩人討論時引用的是當時唯一的 RCT 結果。
- Dwarkesh 對研究量測方式的描述需與研究原文核對，核對結果見 concept note。
