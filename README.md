# review-ml-paper

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Cursor%20%7C%20Codex%20%7C%20Claude%20Code-0A7A3E.svg)](https://agentskills.io)

面向机器学习、数据挖掘与人工智能论文的审稿 Agent Skill。仓库地址为 [JiaweiSheng/review-ml-paper-skill](https://github.com/JiaweiSheng/review-ml-paper-skill)。给定稿件、PDF、摘要、实验部分或已有审稿笔记后，默认输出：

1. 正式英文审稿：`Summary` / `Strengths` / `Weaknesses` / `Questions` / `Typos`
2. 中文 `论文解读`：`任务问题` / `研究动机` / `方法思路` / `实验效果`
3. 与英文审稿对应的中文审稿
4. 文末建议档位：`Accept` / `Weak Accept` / `Weak Reject` / `Reject`

若用户指定仅输出英文或仅输出中文，则按该要求生成；未指定时，默认输出上述英文审稿、中文解读、中文审稿及建议档位。所有针对论文的判断均基于用户提供的材料，不编造结果、基线、引用、章节号或笔误。

## 兼容性

本仓库遵循 [Agent Skills](https://agentskills.io) 开放格式。可执行核心为根目录 `SKILL.md`；中文对照见 [`SKILL.zh.md`](SKILL.zh.md)，供阅读，不参与 Agent 执行。各平台专有配置置于独立文件，以保持可移植部分不受平台字段影响。

| 平台 | 安装位置 | 额外文件 |
| --- | --- | --- |
| Cursor | `~/.cursor/skills/review-ml-paper` | 无 |
| Codex | `~/.codex/skills/review-ml-paper` | `agents/openai.yaml`、`.codex-plugin/` |
| Claude Code | `~/.claude/skills/review-ml-paper` 或插件市场 | `agents/claude.yaml`、`.claude-plugin/` |

GitHub 仓库名为 `review-ml-paper-skill`。安装目录须为 `review-ml-paper`，以与 `SKILL.md` 中的 `name` 字段一致。

## 安装

在 Cursor、Codex 或 Claude Code 的对话中发送：

```text
请安装 https://github.com/JiaweiSheng/review-ml-paper-skill.git
```

Agent 将 skill 安装至对应用户目录。安装完成后，请新开对话再使用。

命令行安装：

```bash
npx skills add JiaweiSheng/review-ml-paper-skill -g
```

### Cursor

```bash
git clone https://github.com/JiaweiSheng/review-ml-paper-skill.git \
  ~/.cursor/skills/review-ml-paper
```

安装完成后，请新开 Agent 对话。更新：

```bash
git -C ~/.cursor/skills/review-ml-paper pull
```

也可通过 `/review-ml-paper` 手动调用，并在 **Customize → Skills** 中确认其位于 **Agent Decides**。

### Codex

```bash
git clone https://github.com/JiaweiSheng/review-ml-paper-skill.git \
  ~/.codex/skills/review-ml-paper
```

更新：

```bash
git -C ~/.codex/skills/review-ml-paper pull
```

Codex 读取 `SKILL.md` 以及 `agents/openai.yaml` 中的显示名称、简介与默认提示。

### Claude Code

安装至个人 Skills 目录：

```bash
git clone https://github.com/JiaweiSheng/review-ml-paper-skill.git \
  ~/.claude/skills/review-ml-paper
```

或通过插件市场安装：

```text
/plugin marketplace add JiaweiSheng/review-ml-paper-skill
/plugin install review-ml-paper
```

## 使用示例

```text
用 review-ml-paper 审这篇论文 @paper.pdf

帮我写会议审稿意见，输出英文审稿、中文论文解读和对应的中文审稿。

只要英文审稿。

只要中文解读和中文审稿。

根据摘要和实验部分写一版审稿，并标明未看到全文。

把这份已有审稿改成 Summary / Strengths / Weaknesses / Questions / Typos 结构。
```

## 输出结构

```text
Summary
Strengths
Weaknesses
Questions
Typos

论文解读
  任务问题
  研究动机
  方法思路
  实验效果

Summary（中文）
Strengths（中文）
Weaknesses（中文）
Questions（中文）
Typos（中文）

Recommendation
  Accept / Weak Accept / Weak Reject / Reject
```

## 仓库结构

```text
.
├── SKILL.md                      # 可移植 Agent Skill 核心
├── SKILL.zh.md                   # SKILL.md 的中文对照（供人阅读）
├── agents/
│   ├── openai.yaml               # Codex / OpenAI UI 元数据
│   └── claude.yaml               # Claude Code 调用元数据
├── .claude-plugin/               # Claude Code 插件与市场清单
├── .codex-plugin/                # Codex 插件清单
├── .agents/plugins/              # Agent Skills 市场清单
├── README.md
└── LICENSE
```

`SKILL.md` 仅保留 Agent Skills 规范中的可移植字段：`name`、`description`、`license`、`compatibility`、`metadata`。Cursor 的 `disable-model-invocation`、Claude 的 `user-invocable` 以及 Codex 的界面文案均不写入该文件，以便三个平台共用同一套审稿指令。

## 设计原则

同时面向作者与元审稿人：先证明读懂，再给可核验的判断。

- 稿件是唯一证据
- 事实、判断、建议分层
- 检查动机–方法–实验是否对齐
- 按不足给出建议，补充讨论或证明，不默认补实验
- 评贡献，不评复杂度
- 坦诚、中立，措辞与证据强度匹配
- 简单句写清意思；优点与缺点每条两三句、一段写完；评分从已写优缺点推出

## 许可证

MIT。详见 [LICENSE](LICENSE)。
