> **PREVIEW** — 預計寫入 `raw/sources/papers/2026-W32-cli-coding-agents-microsoft-rollout.md`
> 尚未寫入 vault。

---

---
type: source
status: raw
domain: ai-workflow
source: arXiv preprint 2607.01418v1 (cs.SE / cs.AI / cs.HC)
author: Emerson Murphy-Hill, Jenna Butler, Alexandra Savelieva
published: 2026-07-03
created: 2026-08-09
processed: true
related_concepts:
  - "[[wiki/concepts/ai-workflow/coding-agent-productivity-proxy-gap]]"
tags: []
---
# Adoption and Impact of Command-Line AI Coding Agents: A Study of Microsoft's Early 2026 Rollout of Claude Code and GitHub Copilot CLI

## Source

- URL：https://arxiv.org/abs/2607.01418　／　HTML 全文 https://arxiv.org/html/2607.01418v1
- 類型：arXiv 預印本，**未經同行評審**
- 授權：CC BY 4.0，Open Access，全文已實讀
- 篇幅：23 頁，10 張圖、3 條計量方程式
- 作者機構：三位皆為 Microsoft
- 資料來源：Microsoft 內部工程遙測（Azure DevOps PR 記錄、工具使用日誌、HR 記錄）＋ Agentic Engineering Day 開放式問卷 609 份

## 原始摘錄 / 摘要

### 論文自陳的定位（原文短引）

- 「the first field study to use developer-level telemetry to analyze both the adoption of agentic command line tools and their effect on pull-request output」

### 研究設計

兩個獨立研究，五個研究問題。

採用研究（RQ1 誰會先試、RQ2 誰會留下來）：
- 預測變數建構期 2025-10-01 至 2026-01-04（13 週）
- 觀察期 2026-01-05 至 2026-04-29（約 17 週）
- RQ1 用工程師-週面板的離散時間邏輯迴歸；RQ2 用採用者橫截面邏輯迴歸
- 留存定義：首次使用後 14 天內至少 5 天有活動
- 控制：週固定效應、部門固定效應，標準誤按工程師聚類

結果研究（RQ3 產出、RQ4 工具差異、RQ5 誰獲益最多）：
- Part 1 用 CausalImpact（貝葉斯結構時間序列），合成反事實由 10 組未使用工具的 PR 創作者建構。Pre 期 2024-10-01 至 2026-01-04（461 天），Post 期 2026-01-05 至 2026-04-29（115 天）
- Part 2 用工程師固定效應泊松迴歸做劑量反應，週使用日數分 {0,1,2,3,4,5+}
- 樣本篩選：pre 期四週內至少 2 個合併 PR；PR 計數取 P5–P95
- 產出定義：28 天內完成合併的 PR

### 主要數值結果

RQ1 初始採用（勝率變化）：

| 預測變數 | 分層 | 效果 |
|---|---|---|
| 跳級同儕使用比例 | 25%+ | +216% |
| 直屬經理使用 | 是 | +82% |
| 先前 IDE Copilot 使用 | 60+ 天 | +83% |
| 先前 IDE Copilot 使用 | 1–14 天 | +49% |
| 評論同儕使用比例 | 25%+ | +54% |
| 基線 PR 活動 | 2+ /週 | +34% |
| 基線 PR 活動 | ≤1 /週 | +19% |
| 職級 | IC5 | +22% |
| 職級 | IC2 / IC3 | −13% / −14% |
| 任職年資 | <1 年 | +11% |

經理職級 M4–M6 無顯著差異；年資除 <1 年外無顯著效應。

RQ2 留存（勝率變化）：

| 預測變數 | 分層 | 效果 |
|---|---|---|
| 基線 PR 活動 | 2+ /週 | +31% |
| 跳級同儕使用比例 | 25%+ | +66% |
| 評論同儕使用比例 | 25%+ | +54% |
| 直屬經理使用 | 是 | +22% |
| 基線 PR 活動 | 1–2 /週 | +14% |
| 基線 PR 活動 | ≤1 /週 | +13% |
| 先前 IDE Copilot 使用 | 所有分層 | −12% 至 −15% |

RQ3 產出：
- CausalImpact：+24.0% 合併 PR/工程師/日，95% CI [+14.5%, +33.7%]，p<0.001
- 分期：2 月 +29.4% [+17.7%, +44.4%]；3–4 月 +20.0% [+7.4%, +35.9%]。區間重疊，無統計顯著衰減
- 安慰劑檢定（2025-10-06 假想介入日）：−1.1% [−10.6%, +8.6%]，通過
- 劑量反應：每週 1 天 +15.0%；每週 5+ 天 +50.1%，曲線單調遞增

RQ4 工具比較（單工具採用者）：
- Claude Code：+11.4% [+9.4%, +13.6%]
- Copilot CLI：+24.9% [+23.0%, +26.8%]
- 差異 2.2 倍，p<0.0001

RQ5 亞群（3 天/週用量，經 Benjamini–Hochberg 校正）：
- IC4 基線 +21.3% [+19.6%, +23.0%]；低階 IC 與高階經理提升較大，呈 C 形
- 年資 5–15 年基線 +21.5% [+19.9%, +23.1%]；<1 年提升最大（作者提醒可能混入入職效應），15+ 年亦較高

### 引言中的成本動機（原文短引）

- Meta 一名員工單月使用量達 2,810 億 token，作者估算「potentially costing $1.4 million alone」

### 質性調查（609 份回應）

作者歸納五個主題，各附代表性引述：

| 主題 | 代表引述（原文） |
|---|---|
| 產出增加 | 「I complete more PRs per week」 |
| 工作性質改變 | 「updating documentation, analyzing it for issues and quality, prototyping app ideas」 |
| 任務選擇改變 | 「larger changes that I never would have taken on in the past」 |
| 雜務自動化 | 「boilerplate plumbing a lot faster」、「repetitive unit tests faster」 |
| 心態轉變 | 「Using GitHub CLI has entirely changed the way that I approach all my projects...I am never going back」 |

另有一位參與者表示其變更中「nearly 100% of the code written by Copilot CLI agent」。

### 論文自陳限制

構念效度：
1. 留存閾值（14 天內 5 天）與 28 天合併窗口皆為武斷選擇。作者以 3-of-14 與 7-of-14 重測，方向一致。
2. 合併 PR 是不完美代理，作者原文列出三項：未測量品質、可能增加複雜性、可能偏好小而頻繁的 PR。

內部效度：
3. 採用研究為橫截面設計，無法排除混淆。
4. 社會效應無法分離同儕影響與同質性（相似的人本來就聚在一起）。
5. 固定效應遺漏工程師特定且時變的衝擊（個人專案、休假）。
6. Part 1 的處理組為自選採用者，合成反事實可能有偏差。
7. Part 2 的劑量反應應視為關聯而非因果，高使用週可能含較輕的任務組合。
8. 單工具限制排除了可能特殊的多工具使用者。

外部效度：
9. 單一公司、單一時間窗（2026 年初）、16 週。作者指出這足以捕捉早期衰減，但無法檢測長期衰減。
10. 只計 Azure DevOps 的 PR，未涵蓋其他生態系統。

研究者位置性：
11. 作者為 Microsoft 員工；Microsoft 銷售 AI 工具、鼓勵使用、擁有 GitHub。作者原文稱無明確壓力，但「鄰近性可能形塑研究問題、設計與詮釋」。

AI 使用披露：
12. 作者以 GitHub Copilot（Claude Opus 4.6–4.8）產出初稿、第 4 與第 5 節全部分析程式碼與圖表，並協助文本重組。研究問題、設計、方法與詮釋為作者決定。

### 結論中的自我設限（原文短引）

- 「The pressing open question is now about quality, whether this added throughput yields better software. The field still lacks agreed-upon measures to answer it.」

## 我自己的註記

- 這篇最誠實的一句話在結論而不在限制章節。作者花 23 頁證明 PR 變多，最後自己說真正的問題是品質，而這個領域還沒有能回答品質的共識指標。
- RQ1 與 RQ2 對 IDE Copilot 老手給出相反的符號。老手更會去試（+83%），試了之後留存卻低 12–15%。作者只給了一句推測：他們有替代選項。這個矛盾是全篇最有價值卻最沒被展開的地方。
- RQ4 的方向對作者不利也對作者有利：說它有利，是因為微軟自家工具勝出 2.2 倍；說它不利，是因為公眾觀感恰好相反，作者自己也承認這點（「despite public perception favoring Claude Code for autonomous work」）。作者列了兩個假說，都沒檢驗。
- 引言用 Meta 那位員工的 2,810 億 token 開場，把整篇框成「值不值得花這個錢」。但全篇沒有任何成本效益計算，結論也只說「輸出是否證明成本合理是價值問題，不是吞吐量問題」。開場的框架與結尾的免責之間有落差。
- 社會擴散那組結果對個人開發者不適用。跳級同儕 +216% 是全篇最大的效果量，而它描述的是一個大型組織內部的傳播機制。

## 待處理問題

- 若把產出指標從「合併 PR 數」換成「合併 PR 的變更行數」或「事後回退率」，+24% 還在嗎？論文沒做這個穩健性檢查。
- 留存低但採用高的 IDE 老手，後來去了哪裡？回到 IDE、還是離開 AI 工具？論文沒追蹤。
- Copilot CLI 對 Claude Code 的 2.2 倍差距，有多少來自任務組合、多少來自組織整合、多少來自工具本身？作者列了假說但無檢驗。

## 處理紀錄

- 2026-08-09：建立 source note（W32 主選）
