# PDF与TeX参考文献及正文核对实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to执行本计划并在各阶段设置检查点。

**Goal:** 用 `第三十五届_冯如杯__主赛道.pdf` 的参考文献替换/校准 `FRBMain.tex` 中的参考文献，并确认 TeX 摘要与正文文本（排除封面、目录等前置内容）与 PDF 一致。

**Architecture:** 以 PDF 文本提取结果作为基准，先按页识别摘要、正文和参考文献范围，再将 TeX 的可见文本与 PDF 做规范化比较。参考文献采用 PDF 的 50 条条目，保留 TeX 的排版结构和换行控制，仅修正条目内容与必要的 TeX 转义。

**Tech Stack:** XeLaTeX source (`FRBMain.tex`), BibTeX-style text, Poppler `pdftotext`/`pdfinfo`, Python 3 标准库脚本。

**Spec:** 用户消息及 `D:\Users\lenovo\Desktop\挑战杯num1\AGENTS.md`（本目录不存在仓库级文件，遵循会话提供的全局规则）。

## Global Constraints

- 不编译、不生成或覆盖 PDF。
- 正文/摘要核对排除封面、目录、页眉页脚、页码和参考文献排版本身。
- 保留现有 TeX 模板结构，仅修改与目标直接相关的内容。
- 所有结论必须有新鲜的文本提取或静态检查证据。

### Task 1: 结构盘点与 PDF 文本提取

**Files:**
- Inspect: `FRBMain.tex`, `references.bib`, `library.bib`, `第三十五届_冯如杯__主赛道.pdf`
- Create/Update: `findings.md`, `progress.md`

- [ ] 确认 TeX 正文入口、摘要范围、参考文献范围及实际使用的引用来源。
- [ ] 用 `pdftotext -layout -enc UTF-8` 提取 PDF，记录页数和摘要/正文/参考文献页。
- [ ] 将页范围和提取限制记录到 `findings.md`。

### Task 2: 摘要与正文规范化对比

**Files:**
- Inspect: `FRBMain.tex` and extracted PDF text
- Create/Update: `findings.md`

- [ ] 去除 TeX 命令、图片环境、页眉页脚、页码和 PDF 断行连字符，保留可见文本。
- [ ] 对比中文摘要、英文摘要和正文各段，逐段记录完全一致、仅排版差异和实质差异。
- [ ] 对任何实质差异定位到 `FRBMain.tex` 行号。

### Task 3: 参考文献替换

**Files:**
- Modify: `FRBMain.tex` 参考文献区域（`参考文献` 标题至 `\end{document}` 前）
- Inspect: `references.bib`, `第三十五届_冯如杯__主赛道.pdf` 参考文献页

- [ ] 按 PDF [1]–[50] 顺序替换条目，修正 PDF 中的标题、作者、出版项、URL、DOI、连字符和引号。
- [ ] 对 TeX 特殊字符执行必要转义（如 `&`、`_`），不改变可见文本。
- [ ] 检查正文引用编号仍覆盖 [1]–[50]，且无悬空或重复编号。

### Task 4: 不编译条件下的最终验证

**Files:**
- Inspect: modified `FRBMain.tex`, `references.bib`, plan logs

- [ ] 用静态脚本重新提取并比较摘要/正文文本。
- [ ] 检查 TeX 环境配对、参考文献编号连续性、未闭合大括号和危险未转义字符。
- [ ] 明确说明未执行编译，因此不对版式或编译产物作保证。
- [ ] 更新 `task_plan.md`、`findings.md`、`progress.md`。
