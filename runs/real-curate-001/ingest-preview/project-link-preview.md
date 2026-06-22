---
# 預覽用 frontmatter，非正式 vault frontmatter
type: output
output_kind: project-link
curation_week: 2026-W26
related_source: "[[raw/sources/articles/2026-W26-coding-agent-era-workflow-survey]]"
related_project: weekly-reading-ingest
domain: ai-workflow
related_domains: []
tags: [weekly-reading, project-link]
created: 2026-06-22
---

> 本檔為 ingest preview，**目標位置：`wiki/outputs/weekly-reading/project-links/`**。本輪未實際寫入 vault。
>
> 重要：`wiki/projects/` 目前**沒有** `weekly-reading-ingest` 專案資料夾，因此本檔**不建立任何 wikilink 指向 `wiki/projects/weekly-reading-ingest/...`**（該路徑不存在,不得假造）。本檔只是 `wiki/outputs/weekly-reading/project-links/` 底下的一篇獨立筆記,以純文字描述關聯到工具專案 `D:\ClaudeCode\projects\weekly-reading-ingest\`,不連結任何 vault 內路徑。

# A Survey of Development Workflows in the Coding Agent Era — Project Link（Preview）

## 關聯專案

`weekly-reading-ingest`（本工具專案，位於 `D:\ClaudeCode\projects\weekly-reading-ingest\`，非 vault 內專案，目前在 vault 的 `wiki/projects/` 沒有對應資料夾）。

## 為什麼相關

本文提出的「AGENTS.md 設計檢查清單」與「會話設計複雜度光譜」直接可用來檢查本工具現有的兩份 skill 文件：

- **如何用來檢查 `weekly-reading-curate/SKILL.md`**：用「文件大小 60–150 行」與「分層載入（常駐/激活時/按需）」兩個條件檢查目前職責、嚴禁、候選報告格式、結束狀態四個區塊是否該分層；目前篇幅與規則密度仍屬可控,可作為定期複查基準,而非立即需要改動。
- **如何用來檢查 `weekly-reading-ingest/SKILL.md`**：此檔因疊加多輪 patch（Domain Decision、Free Access 二次攔截、低分備選改選警示、Safety Checklist、狀態機）篇幅已明顯變長,是最值得用「會話設計複雜度光譜」重新定位的對象——目前的規則密度接近原文光譜中「中等複雜度」位置（多個明確分支判斷,但尚未到多智能體協作），可考慮日後是否要把 Safety Checklist 拆成獨立參考層,而不是全部留在常駐指令層。

## Skill 邊界與 curate/ingest 分離檢查

用本文框架反過來檢查本工具現有的兩階段設計：

- **skill 邊界是否清楚**：`weekly-reading-curate` 的「嚴禁」清單明確列出「不得寫入 vault」「不得建立四類筆記」，`weekly-reading-ingest` 的「觸發條件」明確限定只接受三種確認語句——兩份文件各自的職責邊界用條列方式寫死，符合文中「驗證規則應可機械檢查、不只是文字提醒」的精神，目前邊界算清楚，沒有發現職責重疊或遺漏的縫隙。
- **curate 與 ingest 是否分離**：是，且分離方式恰好對應本文核心立場——「人機協作應在明確審查點介入，而非持續監控」。curate 永遠不寫 vault、ingest 永遠需要明確確認語句才觸發，中間的「等待確認」狀態就是文中所說的審查點，這是本工具與原文設計理念吻合度最高的一處，值得在 concept note 的「使用場景」之外另外記一筆,但本輪不展開,先記錄在此。

## 可能的應用方式

- 下一輪可考慮：用 AGENTS.md 檢查清單的「驗證規則」概念（路徑存在性檢查、過期偵測）,檢查 Safety Checklist 裡的條目是否都還對應 vault 目前的實際路徑與規則（例如 `allowedConceptDomains`、`allowedSourceFolders` 是否與 config 同步）。
- 「會話設計複雜度光譜」可用來決定：未來若要新增更多 ingest 情境（例如多語言來源、多專案關聯),應該用更多分支條件,還是拆成獨立 skill。

## 不應該直接套用的地方

- 原文提到的「19 個智能體（oh-my-claudecode）」等具體工具組合**不應該**被當作本工具的目標架構參考——本工具刻意保持單一 curate + 單一 ingest 兩個 skill 的簡單結構,原文那類多智能體系統是為更大型協作場景設計,套用到私人單人工具是不必要的複雜度。
- 原文「60–150 行」是作者個人經驗建議,不是量化驗證過的標準,不應該不假思索地當作本工具 SKILL.md 長度的硬性指標,只能當參考起點。
- 原文許多 context engineering 失敗模式案例來自團隊協作場景（多人審查、CI 整合）,本工具是純個人單機流程,部分緩解策略（如「破壞性操作阻止」的團隊權限設計）不直接適用,需要簡化後才能套用。
