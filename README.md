# AI Skills

通用 AI 技能库——每个 skill 是一份结构化工作流文档（`SKILL.md`），可喂给任何支持 Markdown 和指令跟随的大模型。

**核心理念：** 将高频任务的提示词工程封装为文件，一次编写、反复使用、版本管理、团队共享。

## 快速开始

```bash
git clone https://github.com/<user>/ai-skills.git
```

## 目录结构

```
.skills/
├── README.md
└── academic-paper-prompt-workflow/
    └── SKILL.md
```

> 部分 skill 目录下可能附带 `*-clean.md` 等保留副本，仅供维护者参考，使用者只需关注 `SKILL.md`。

## 已收录 Skill

### academic-paper-prompt-workflow

从零散需求到标准格式 DOCX 的学术论文全流程。

**四种模式：**

| 模式 | 输入 → 输出 |
|---|---|
| Prompt-only | 主题/观点/文献 → 标准化写作提示词 |
| Prompt + Markdown | 提示词自注入 → Markdown 论文正文 |
| Markdown to DOCX | 已有 Markdown → python-docx 直出标准论文格式 |
| Full pipeline | 全自动：需求 → 提示词 → Markdown → DOCX → 四重校验 |

**格式规范覆盖：** 中文摘要 / 英文摘要 / 自动目录 / 正文（四级标题）/ 图表公式题注 / 参考文献 / 致谢 / 附录。分节页码（前置罗马 + 正文阿拉伯）、TOC 域、乱码检测。

## 兼容性

`SKILL.md` 本质为结构化 Prompt，可在支持系统指令或自定义 Agent 的任意大模型工具中使用。

### 一、原生支持（自动加载）

将本仓库 clone 至对应目录，工具启动时自动发现并注册：

| 工具 | 安装路径 |
|---|---|
| Claude Code | `~/.skills/`（macOS/Linux）或 `%USERPROFILE%\.skills\`（Windows） |

### 二、网页端 AI（直接粘贴 / 自定义助手）

打开 `SKILL.md`，去掉顶部 `---` 包裹的元数据块，将正文粘贴到对话开头；或创建自定义助手/智能体，填入 Instructions。

| 分类 | 工具 |
|---|---|
| 国外 | ChatGPT、Claude、Gemini、Perplexity AI |
| 国内 | 文心一言、通义千问、讯飞星火、智谱清言、Kimi、豆包 |

### 三、Agent / 工作流工具（需结构化）

将 `SKILL.md` 拆分为 Role（角色）、Workflow（流程）、Constraints（约束），填入对应配置项。

| 分类 | 工具 |
|---|---|
| 国外 | LangChain、AutoGen、CrewAI、Flowise |
| 国内 | Dify、Coze、FastGPT、Trae |

### 四、API / 开发环境

将 `SKILL.md` 正文作为 system message 传入：

```json
{
  "messages": [
    {"role": "system", "content": "<SKILL.md 正文>"},
    {"role": "user", "content": "<用户输入>"}
  ]
}
```

适用：OpenAI API、Anthropic API、Gemini API、文心大模型 API、通义千问 API、智谱 AI API 等。

## 添加新 Skill

```
.skills/
└── your-skill-name/
    └── SKILL.md
```

`SKILL.md` 最小格式：

```markdown
---
name: your-skill-name
description: 做什么、何时触发，一句话
---

# Your Skill Title

面向 AI 模型的工作流指令……
```

贡献流程：新建目录 → 编写 SKILL.md → `git add` → `git commit` → `git push`。

## License

MIT
