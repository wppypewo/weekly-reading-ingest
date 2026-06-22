---
# 預覽用 frontmatter，非正式 vault frontmatter
type: output
output_kind: review-card
curation_week: 2026-W26
related_source: "[[raw/sources/articles/2026-W26-coding-agent-era-workflow-survey]]"
domain: ai-workflow
related_domains: []
tags: [weekly-reading, review-card]
question_count: 2
created: 2026-06-22
---

> 本檔為 ingest preview，**目標位置：`wiki/outputs/weekly-reading/review-cards/`**。本輪未實際寫入 vault。最多 2 題，未硬湊第 3 題。

# A Survey of Development Workflows in the Coding Agent Era — Review Card（Preview）

> 來源：[[raw/sources/articles/2026-W26-coding-agent-era-workflow-survey]]

## Q1

套用文中「會話設計複雜度光譜」（1 行 bash 迴圈 → `/loop` 指令 → FIC 方法 → 雙智能體 → 19 個智能體的多代理系統），目前 `weekly-reading-curate` 與 `weekly-reading-ingest` 兩個 skill 分別落在光譜的哪個位置？是否已經過度複雜？

**為什麼這題有價值**：檢查「判斷」與「應用」。這不是在問原文寫了什麼,而是要求把抽象光譜實際套到自己正在維護的兩份文件上做定位判斷——尤其 `weekly-reading-ingest` 因多輪 patch（Domain Decision、Free Access 攔截、低分備選警示）已經有多個分支,值得用這個框架自我檢視是否該拆層或簡化。

## Q2

如果 AGENTS.md / SKILL.md 設計建議保持精簡（60–150 行），但 Safety Checklist 又必須完整覆蓋既有規則（domain 限制、free access 攔截、寫入範圍等），哪些規則**不能**因為「縮短篇幅」而被犧牲？

**為什麼這題有價值**：檢查「判斷」與「連結既有知識」。這題逼著使用者在「精簡」與「規則完整性」兩個互相拉扯的目標之間做優先序判斷,而不是單純複述文章建議,且直接連回本工具現有 Safety Checklist 的實際內容（例如不可寫 `meta/index.md`、不可改 `tools/kb/*.mjs` 這類紅線規則,理論上不該因為精簡而被移除或弱化）。
