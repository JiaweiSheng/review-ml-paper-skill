# review-ml-paper

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](CHANGELOG.md)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Cursor%20%7C%20Codex%20%7C%20Claude%20Code-0A7A3E.svg)](https://agentskills.io)

面向机器学习、数据挖掘、人工智能论文的审稿 Agent Skill。给定稿件、PDF、摘要、实验部分或已有审稿笔记后，默认生成：

1. 正式英文审稿：`Summary` / `Strengths` / `Weaknesses` / `Questions` / `Typos`
2. 中文 `论文解读`：`任务问题` / `研究动机` / `方法思路` / `实验效果`
3. 与英文审稿完全对应的中文审稿
4. 文末四档建议：`Accept` / `Weak Accept` / `Weak Reject` / `Reject`

用户明确只要英文或只要中文时，按用户要求输出；未说明则默认上述三件套加建议档位。所有针对论文的判断都基于用户提供的材料，不编造结果、基线、引用、章节号或笔误。

## 兼容性

本仓库遵循 [Agent Skills](https://agentskills.io) 开放格式。可执行核心是根目录的 `SKILL.md`；中文对照见 [`SKILL.zh.md`](SKILL.zh.md)，供中文使用者阅读，不参与 Agent 执行。各平台专有信息放在独立文件里，避免污染可移植部分。

| 平台 | 安装位置 | 额外文件 |
| --- | --- | --- |
| Cursor | `~/.cursor/skills/review-ml-paper` | 无（读取 `SKILL.md`） |
| Codex | `~/.codex/skills/review-ml-paper` | `agents/openai.yaml`、`.codex-plugin/` |
| Claude Code | `~/.claude/skills/review-ml-paper` 或插件市场 | `agents/claude.yaml`、`.claude-plugin/` |

克隆时目标目录必须名为 `review-ml-paper`，以便与 `SKILL.md` 中的 `name` 一致。

如果仓库地址不是 `JiaweiSheng/review-ml-paper`，把下面命令里的 GitHub URL 换成你的仓库即可。

## 安装

### Cursor

```bash
git clone https://github.com/JiaweiSheng/review-ml-paper.git \
  ~/.cursor/skills/review-ml-paper
```

新开一个 Agent 对话后即可使用。更新：

```bash
git -C ~/.cursor/skills/review-ml-paper pull
```

也可在聊天中输入 `/review-ml-paper` 手动调用。可在 **Customize → Skills** 中确认它出现在 **Agent Decides**。

### Codex

```bash
git clone https://github.com/JiaweiSheng/review-ml-paper.git \
  ~/.codex/skills/review-ml-paper
```

更新：

```bash
git -C ~/.codex/skills/review-ml-paper pull
```

Codex 会读取 `SKILL.md` 和 `agents/openai.yaml` 中的显示名称、简介与默认提示。

### Claude Code

个人 Skills 目录：

```bash
git clone https://github.com/JiaweiSheng/review-ml-paper.git \
  ~/.claude/skills/review-ml-paper
```

或作为插件市场安装：

```text
/plugin marketplace add JiaweiSheng/review-ml-paper
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
├── LICENSE
└── CHANGELOG.md
```

`SKILL.md` 只保留 Agent Skills 规范中的可移植字段：`name`、`description`、`license`、`compatibility`、`metadata`。Cursor 的 `disable-model-invocation`、Claude 的 `user-invocable`、Codex 的界面文案都不写进该文件，因此三个平台可以共用同一份审稿指令。

## 设计原则

- 未说明语言时，先写英文正式审稿，再写中文解读，最后写对应中文审稿；用户只要英文或只要中文时，按用户要求。
- 每条优点和缺点都要落到稿件证据上；缺点写成流畅段落，不用 `Issue:` 一类标签。
- 缺实验不是默认补救方式；讨论、澄清、现有结果分析或理论说明可能已经足够。
- 不把方法复杂当成优点，也不因为方法简单就否定。
- 只记录核实过的笔误；来源不足时写 `None noted.`
- 审稿意见之后给出四档建议：接受、弱收、弱拒、拒绝。

## 许可证

MIT. See [LICENSE](LICENSE).
