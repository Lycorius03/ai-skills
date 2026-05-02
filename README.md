# AI Skills

通用 AI 技能库。每个 skill 是一份已结构化的 `SKILL.md`，可直接喂给大模型使用。

## 快速开始

```bash
git clone https://github.com/Lycorius03/ai-skills.git
```

### 网页端 AI

`SKILL.md` 本身即 Markdown，直接复制全文粘贴到对话开头即可。

适用：ChatGPT、Claude、Gemini、Perplexity AI、文心一言、通义千问、讯飞星火、智谱清言、Kimi、豆包

### API 调用

将 `SKILL.md` 正文作为 system message 传入：

```json
{"role": "system", "content": "<SKILL.md 正文>"}
```

适用：OpenAI API、Anthropic API、Gemini API、文心大模型 API、通义千问 API、智谱 AI API

### Agent / 工作流平台

在创建 Agent 或自定义助手时，将 `SKILL.md` 正文粘贴到系统提示词（System Prompt / Instructions）配置项中。

适用：Dify、Coze、FastGPT、Trae、LangChain、AutoGen、CrewAI、Flowise

### Claude Code（自动加载）

将本仓库 clone 到 skills 目录，启动时自动发现：

| 平台 | 路径 |
|---|---|
| macOS / Linux | `~/.skills/` |
| Windows | `%USERPROFILE%\.skills\` |

## 已收录 Skill

### academic-paper-prompt-workflow

从零散需求到标准格式 DOCX 的学术论文全流程。

| 模式 | 说明 |
|---|---|
| Prompt-only | 输入主题/观点/文献 → 输出标准化写作提示词 |
| Prompt + Markdown | 提示词自注入 → 生成 Markdown 论文 |
| Markdown to DOCX | 已有 Markdown → python-docx 直出标准论文格式 |
| Full pipeline | 全自动：需求 → 提示词 → Markdown → DOCX → 四重校验 |

**格式规范：** 中文摘要 / 英文摘要 / 自动目录 / 正文（四级标题）/ 图表公式题注 / 参考文献 / 致谢 / 附录。分节页码（前置罗马 + 正文阿拉伯）、TOC 域、乱码检测。

## 贡献新 Skill

```
.skills/
└── your-skill-name/
    └── SKILL.md
```

`SKILL.md` 格式：

```markdown
---
name: your-skill-name
description: 做什么、何时触发
---

# Your Skill Title

面向 AI 模型的工作流指令……
```

```bash
git add your-skill-name/
git commit -m "feat: add your-skill-name skill"
git push
```

## License

MIT
