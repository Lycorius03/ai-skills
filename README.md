# Claude Code Skills

个人 Claude Code 技能库。每个子目录为一个独立 skill，放置后 Claude Code 会自动发现并加载。

## 目录结构

```
.skills/
├── README.md                           ← 本文件
└── academic-paper-prompt-workflow/     ← 学术论文全流程
    ├── SKILL.md                        ← 正式 skill（Claude Code 加载用）
    └── academic-paper-prompt-workflow-SKILL-clean.md  ← 原始精修版
```

## 已注册 Skill

### academic-paper-prompt-workflow

学术论文从零散需求到标准格式 DOCX 的全流程管线。

| 模式 | 说明 |
|---|---|
| Prompt-only | 输入主题/观点/文献 → 输出标准化写作提示词 |
| Prompt + Markdown | 提示词自注入 → 生成 Markdown 论文 |
| Markdown to DOCX | 已有 Markdown → python-docx 直出标准论文格式 |
| Full pipeline | 全自动：需求 → 提示词 → Markdown → DOCX → 校验 |

**格式规范覆盖：** 中文摘要 / 英文摘要 / 自动目录 / 正文（四级标题）/ 图表公式题注 / 参考文献 / 致谢 / 附录，含分节页码（前置罗马、正文阿拉伯）、TOC 域、乱码检测。

## 使用方式

将此仓库 clone 到 `F:\.skills\`（Windows）或 `~/.skills/`（Linux/macOS），Claude Code 启动时自动加载。

```bash
git clone <your-repo-url> /path/to/.skills
```

## 添加新 Skill

1. 在 `.skills/` 下新建子目录 `my-skill/`
2. 在其中创建 `SKILL.md`（含 frontmatter name 和 description）
3. Push 到仓库

```yaml
# SKILL.md 最小示例
---
name: my-skill
description: What this skill does and when to use it
---

# My Skill

Instructions for the agent...
```
