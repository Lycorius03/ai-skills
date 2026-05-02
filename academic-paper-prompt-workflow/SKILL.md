---
name: academic-paper-prompt-workflow
description: Use this skill when an agent must turn sparse paper requirements into a reusable academic writing prompt, optionally self-inject that prompt to generate a Markdown paper, and/or convert the Markdown into a correctly formatted DOCX thesis with automatic TOC, sectioned page numbers, citation discipline, and repeated anti-garbled-text checks.
---

# Academic Paper Prompt Workflow

Use this skill for Chinese or bilingual academic paper workflows. It supports three connected tasks:

- Generate a final paper-writing prompt from user inputs.
- Self-inject that prompt to produce a Markdown academic paper.
- Convert the Markdown paper into a standard formatted DOCX thesis/paper.

## Modes

Choose the mode from the user request:

- **Prompt-only**: output only the final reusable prompt.
- **Prompt + Markdown**: build the prompt internally, self-inject it, and output the Markdown paper.
- **Markdown to DOCX**: convert an existing Markdown paper into a formatted DOCX and verify it.
- **Full pipeline**: collect requirements -> generate prompt -> produce Markdown -> convert to DOCX -> verify.

If the paper topic is missing, ask one concise question. For other missing inputs, make conservative assumptions and state them only when useful.

## Input Extraction

Extract these fields from structured or unstructured user input:

```text
论文主题：required
核心观点：optional; if absent, use “无”
参考文献链接/题名：optional; CNKI, DOI, official pages, URLs, or plain titles
老师要求：optional; if absent, use “无”
字数/篇幅：optional
专业/课程：optional
输出目标：Prompt / Markdown / DOCX / full pipeline
格式规范：optional; if provided, must override defaults
```

Preserve exact reference links, titles, teacher requirements, and formatting rules.

## Citation And Source Integrity

Never fabricate authors, journal names, issue numbers, page ranges, data, empirical findings, or policy facts.

When browsing/searching is available and allowed:

1. Verify references through CNKI, DOI pages, journal sites, university repositories, publisher pages, or official policy/data pages.
2. Prefer primary and official sources.
3. If a reference cannot be accessed, search by exact title.
4. Mark unverifiable items as usable only as topic clues.

When browsing is unavailable:

- Treat provided links/titles as “must-prioritize reference clues”.
- Allow title-level thematic inference.
- Do not invent concrete bibliographic metadata or conclusions.

## Final Prompt Generator

When asked to generate a paper-writing prompt, output a complete prompt using this skeleton.

```text
你是一名严谨的学术论文写作专家，请根据以下信息撰写一篇结构完整、逻辑递进、可转换为 Word 的 Markdown 学术论文。

【论文主题】
[主题]

【核心观点】
[核心观点；如果原始输入为“无”，这里写由你补全的研究主线]

【必须优先使用的参考文献/资料线索】
[逐条列出用户提供或已核验的文献链接、题名、政策文件、数据来源]

【老师要求】
[老师要求；如无，则写“按标准学术论文规范：结构完整、论证清晰、引用规范、语言学术化、不得编造数据。”]

【写作任务】
请围绕论文主题形成一条清晰研究主线，并完成一篇 Markdown 格式论文。论文应体现“问题提出—文献回应—机制解释—对比分析—风险识别—对策提出—结论收束”的递进逻辑，不得写成资料拼接或段落堆砌。

【结构要求】
请严格使用以下结构：
# 标题
## 摘要
## 关键词
## 一、引言
## 二、文献综述
## 三、理论/机制分析
## 四、优势或应用分析
## 五、风险/问题分析
## 六、对策与优化路径
## 七、结论
## 参考文献

【内容要求】
1. 如果核心观点不足，请自动补全合理研究主线，但必须与主题一致。
2. 摘要应概括研究背景、研究问题、分析视角、主要观点与结论。
3. 引言应说明研究背景、现实意义、研究问题和文章结构。
4. 文献综述不能罗列文献，要归纳研究脉络、已有贡献和不足。
5. 理论/机制分析要解释现象背后的因果逻辑或作用路径。
6. 必须加入对比分析，例如“优势 vs 风险”“制度收益 vs 执行成本”“短期效果 vs 长期影响”。
7. 风险/问题分析必须与前文机制相互呼应。
8. 对策建议必须针对前文问题，避免空泛口号。
9. 结论应回扣主题，概括发现，并指出局限或未来研究方向。

【引用规范】
1. 使用 Markdown 脚注格式，如 `[^1]`。
2. 必须优先基于提供的参考文献/资料线索。
3. 如果允许联网检索，可自动寻找 CNKI、官方文件、期刊网页、DOI 或高校库中的真实文献，但必须反复确认文献真实存在。
4. 如果参考文献无法访问，可以基于题名合理推断其相关主题，但不得编造作者、期刊、年份、页码、具体数据或文献结论。
5. 涉及政策、年份、统计数据、机构表述时，必须使用审慎措辞；无法确认的数据不得写成确定事实。

【写作风格】
1. 使用正式、客观、学术化表达。
2. 段落之间必须有承接关系，避免拼接式写作。
3. 不使用口语化表达，不使用夸张判断。
4. 对不确定信息使用“可能”“倾向于”“有待进一步验证”等审慎表达。

【输出格式】
1. 只输出 Markdown 正文。
2. 标题层级使用 `#`、`##`、`###`。
3. 参考文献以 Markdown 脚注形式列出。
4. 保持格式可被 Pandoc 转换为 DOCX。
```

For prompt-only requests, output only the completed prompt.

## Self-Injection Markdown Workflow

When asked to generate the Markdown paper:

1. Build the final prompt from the template.
2. Internally execute that prompt.
3. Draft Markdown with clean heading levels.
4. Use Markdown footnotes `[^n]` for citations.
5. Keep claims evidence-conscious and avoid invented facts.
6. Run the Markdown quality checklist before delivery.

### Markdown Quality Checklist

- Title matches the topic.
- Abstract and keywords are present.
- Required sections are present.
- Literature review synthesizes rather than lists.
- There is explicit contrastive analysis.
- Risks/problems connect to the mechanism analysis.
- Countermeasures respond to identified problems.
- Footnotes use `[^n]` syntax.
- No fabricated reference metadata appears.
- No garbled text markers appear.

## Markdown To DOCX Thesis Workflow

Use this section when the user provides a Markdown paper and asks to convert it into a correctly formatted DOCX thesis/paper.

### 1. Read Source Safely

Always read Markdown as UTF-8 first. If text appears garbled in a shell preview, verify with a UTF-8-aware reader before modifying content.

Check:

- title;
- Chinese abstract and keywords;
- English abstract and key words, if present;
- heading hierarchy;
- tables, figures, equations;
- footnotes/references;
- teacher formatting requirements.

If English Abstract is required but missing, translate the Chinese abstract faithfully. Do not add new empirical claims.

### 2. Default DOCX Structure

Unless the user provides a different standard, produce:

1. 中文摘要 section
2. Abstract section
3. 自动目录 section
4. 正文 section
5. 参考文献 section
6. 致谢/附录 only if source content exists or user explicitly asks

Use Word sections so front matter and body can have different page number formats.

### 3. Standard Formatting Rules

Apply user-provided rules first. If the user gives the following common thesis standard, implement it exactly:

**Chinese Abstract**

- Header: 宋体五号, centered.
- Title “摘要”: 黑体小三, centered; before 30 pt, after 30 pt, exact line spacing 20 pt.
- Body: 宋体小四; before 6 pt; exact line spacing 20 pt; first-line indent 2 Chinese characters.
- Keywords: blank line before; flush left; “关键词：” bold; 宋体小四; before 6 pt; exact line spacing 20 pt.
- Footer: lowercase Roman page number, 宋体五号, centered.

**English Abstract**

- Header: Times New Roman 五号, centered.
- Title “Abstract”: Times New Roman 小三, centered; before 30 pt, after 30 pt, exact line spacing 20 pt.
- Body: Times New Roman 小四; before 6 pt; exact line spacing 20 pt; first-line indent 1 character.
- Key words: blank line before; flush left; “Key words:” bold; Times New Roman 小四; before 6 pt; exact line spacing 20 pt.
- Footer: lowercase Roman page number, centered.

**Table of Contents**

- Header: 宋体五号, centered.
- Title “目录”: 宋体小二, centered; before 30 pt, after 30 pt.
- Content must be a real Word automatic TOC field, clickable after Word updates fields.
- TOC content: 宋体小四; exact line spacing 20 pt; justified.
- Footer: lowercase Roman page number, centered.

**Body**

- Header: 宋体五号, centered; use paper title or chapter title.
- Footer: Arabic page number, 宋体五号, centered.
- Chapter title: 黑体小三, centered; before 30 pt, after 30 pt.
- First-level section title, such as `1.1`: 黑体四号; before 18 pt, after 18 pt.
- Second-level section title, such as `1.1.1`: 黑体小四; before 12 pt, after 12 pt.
- Third-level section title: 黑体小四; before 6 pt, after 6 pt.
- Body text: Chinese 宋体小四; English Times New Roman 小四; before 6 pt; exact line spacing 20 pt; first-line indent 2 Chinese characters.
- Prefer page breaks between major chapters.

**Figures, Tables, Equations**

- Figure title below figure, centered, 宋体五号, before/after 6 pt.
- Figure data source at lower left.
- Table title above table, centered, 宋体五号, before/after 6 pt.
- Table data source at lower left.
- Equation centered; equation number right-aligned as `(1)`; no dash between equation and number.

**References**

- Header: 宋体五号, centered.
- Title “参考文献”: 黑体小三, centered; before 30 pt, after 30 pt.
- Reference body: Chinese 宋体五号; English Times New Roman 五号; exact line spacing 17 pt.
- Use one consistent style, preferably GB/T 7714, APA, or IEEE.
- Arabic page number continues from body.

**Acknowledgements / Appendix**

- Include only when source content exists or user asks.
- Title: 黑体小三, centered; before 30 pt, after 30 pt.
- Body follows normal body text rules.
- Arabic page number continues.

Size mapping:

```text
小二 = 18 pt
小三 = 15 pt
四号 = 14 pt
小四 = 12 pt
五号 = 10.5 pt
```

### 4. DOCX Generation Requirements

When using Python, prefer `python-docx` for deterministic formatting. Use direct OOXML fields where needed:

- page number field: `PAGE`;
- automatic TOC field: `TOC \o "1-3" \h \z \u`;
- section page-number type: lowercase Roman for front matter, decimal for body;
- restart body page number at 1 unless the user requires continuous numbering.

After creating the DOCX, open it in Microsoft Word or LibreOffice to update fields. In Word automation, update all fields and all tables of contents, then save.

### 5. Verification Requirements

Before delivering the DOCX, run repeated checks:

1. **Structural check**
   - DOCX opens successfully.
   - Sections exist for abstract, abstract English, TOC, body.
   - TOC field exists.
   - TOC has clickable hyperlinks after field update.
   - Heading styles are used for TOC entries.
   - Page numbering switches from Roman to Arabic correctly.

2. **Completeness check**
   - Compare source Markdown headings with DOCX headings.
   - Confirm references/footnotes are present.
   - Confirm final source paragraph appears in DOCX/PDF extraction.
   - Confirm table/figure/equation counts match or intentionally explain differences.

3. **Garbled-text check**
   Scan DOCX-extracted text and, if possible, exported PDF text for common mojibake markers. Store the marker list as escaped Unicode strings in scripts to avoid contaminating this skill file:
   ```text
   \uFFFD, \u93C2, \u9365, \u9470, \u95AB, \u7ECC, \u9225, \u7039, \u699B, \u6FEE, \u00C3, \u00C2, \u00E6, ???
   ```
   Any nonzero result must trigger re-reading source as UTF-8 and regenerating/fixing the affected content.

4. **Visual/render check**
   - Prefer rendering DOCX to PDF/PNG using LibreOffice or Word export.
   - Inspect representative pages: abstract, TOC, first body page, table page, references.
   - If rendering tools are unavailable, state that visual PNG QA could not be completed, but still report structural and text checks.

### 6. Delivery Rules

For DOCX requests:

- Deliver the final `.docx` path/link.
- Mention only relevant verification results.
- Do not deliver intermediate PDFs/PNGs unless asked.
- If visual rendering was impossible, say so plainly.

## Anti-Garbled-Text Policy

For every mode, check for mojibake before final output. Common causes:

- reading UTF-8 Markdown through a legacy console code page;
- writing UTF-8 text as ANSI/GBK;
- copying text from a garbled shell preview.

If any marker appears, do not trust the preview. Re-read the original file with explicit UTF-8 and regenerate.

## Minimal Output Policy

- If asked for a prompt, output only the prompt.
- If asked for Markdown, output only the Markdown unless the user asks to see the prompt.
- If asked for DOCX, output the final DOCX and a brief verification note.
- If asked to update this skill, edit `SKILL.md` directly and verify it has no garbled text markers.
