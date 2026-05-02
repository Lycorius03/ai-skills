# AI Skills

通用 AI 技能库——每个 skill 是一个独立的、可复用的 AI 工作流，面向所有支持 Markdown 渲染和指令跟随的大模型（Claude Code、ChatGPT、Gemini、Copilot Chat 等）。

**核心理念：** 将高频任务的提示词工程封装为标准化 skill 文件，一次编写、反复使用、团队共享。

## 目录结构

```
.skills/
├── README.md                                       ← 本文件
└── academic-paper-prompt-workflow/                  ← 学术论文全流程
    ├── SKILL.md                                     ← skill 主文件
    └── academic-paper-prompt-workflow-SKILL-clean.md  ← 精修版副本
```

## 已收录 Skill

### academic-paper-prompt-workflow

学术论文从零散需求到标准格式 DOCX 的全流程管线。

| 模式 | 说明 |
|---|---|
| Prompt-only | 输入主题/观点/文献 → 输出标准化写作提示词 |
| Prompt + Markdown | 提示词自注入 → 生成 Markdown 论文 |
| Markdown to DOCX | 已有 Markdown → python-docx 直出标准论文格式（含分节页码、自动目录、乱码检测） |
| Full pipeline | 全自动：需求 → 提示词 → Markdown → DOCX → 校验 |

**格式规范覆盖：** 中文摘要 / 英文摘要 / 自动目录 / 正文（四级标题）/ 图表公式题注 / 参考文献 / 致谢 / 附录。分节页码（前置罗马+正文阿拉伯）、TOC 域、四重校验（结构/完整性/乱码/渲染）。

## 使用方式

每个 skill 的核心文件是 `SKILL.md`，包含 frontmatter 元数据和完整指令：

### 在 Claude Code 中

将本仓库 clone 到 `~/.skills/`（macOS/Linux）或 `F:\.skills\`（Windows），Claude Code 启动时自动发现并加载：

```bash
git clone <repo-url> /path/to/.skills
```

### 在其他 AI 工具中

直接复制 `SKILL.md` 的正文内容作为 system prompt 或对话初始指令，模型按其中的工作流执行。

### 手动参考

打开 `SKILL.md` 阅读工作流逻辑，人工按步骤执行。

## 贡献新 Skill

1. 在根目录下新建子目录 `your-skill-name/`
2. 在其中创建 `SKILL.md`

```markdown
---
name: your-skill-name
description: 一句话描述这个 skill 做什么、何时触发
---

# Your Skill Title

清晰的工作流指令，面向 AI 模型可执行。
```

3. 提交并推送

## License

MIT
