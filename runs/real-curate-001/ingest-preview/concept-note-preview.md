---
# 預覽用 frontmatter，非正式 vault frontmatter
type: concept
status: evergreen
domain: ai-workflow
confidence: medium
source_notes: ["[[raw/sources/articles/2026-W26-coding-agent-era-workflow-survey]]"]
created: 2026-06-22
updated: 2026-06-22
tags: [weekly-reading]
---

> 本檔為 ingest preview，**目標位置：`wiki/concepts/ai-workflow/agents-md-design-checklist.md`**。本輪未實際寫入 vault。只產 1 篇 concept note，不拆成 3 篇。

# AGENTS.md / Skill 文件設計檢查清單

## 核心結論

讓 agent 不迷路、不膨脹、不遺漏 safety rules 的指引文件（AGENTS.md / CLAUDE.md / SKILL.md），應同時滿足三個結構性條件：**篇幅可控**（建議 60–150 行）、**規則可驗證**（路徑存在性、過期偵測等可機械檢查的條件，而非僅靠文字提醒）、**分層載入**（常駐元資料 / 激活時指令 / 按需資源三層分開，而非一份文件全部塞在同一層級）。

## 背後原因

文件過長會稀釋 agent 對關鍵規則的注意力；規則只用文字描述而無法驗證，容易在多輪修改後悄悄失效（例如過期的路徑引用、過期的決策依據）；不分層會導致每次載入都帶進大量與當下任務無關的內容，浪費 context 預算。

## 使用場景

設計或審查任何 agent 的指引文件時：新建 skill/SKILL.md、CLAUDE.md 全域規則、專案層級 AGENTS.md，或在文件因多輪 patch 疊加而變得臃腫時，用這三個條件檢查是否該精簡或重構。

## 與我目前專案 / 投資 / 學習的關係

直接適用於本工具 `weekly-reading-ingest` 自身：

- `weekly-reading-curate/SKILL.md` 目前篇幅與規則密度尚屬可控，可用此檢查清單定期複查。
- `weekly-reading-ingest/SKILL.md` 因為疊加多輪 patch（domain decision、free access 二次攔截、低分備選警示），篇幅已明顯變長，是最值得用「篇幅可控」與「分層載入」兩個條件重新檢查的對象——哪些規則該留在常駐層、哪些可以移到「按需參考」層，是下一輪可以討論的方向（本輪不展開）。

## 來源

- [[raw/sources/articles/2026-W26-coding-agent-era-workflow-survey]]

## 未確認 / 待查證

- 「60–150 行」是否適用於本工具的 SKILL.md，還是該依規則密度（如 safety checklist 條目數）另訂標準，原文未進一步說明,屬作者個人經驗判斷,非量化驗證過的數字。

## 相關概念

- （暫無，本次為首次 ingest 此 domain 下與此主題相關的概念）
