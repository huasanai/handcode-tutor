> 🌐 **English version**: [README.en.md](./README.en.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Made with Claude Code](https://img.shields.io/badge/Made_with-Claude_Code-d97706)](https://docs.claude.com/en/docs/claude-code/overview)
[![Skills compatible](https://img.shields.io/badge/Skills-compatible-10a37f)](https://www.skills.sh/)
[![Version](https://img.shields.io/github/v/tag/huasanai/handcode-tutor?label=version)](https://github.com/huasanai/handcode-tutor/tags)

<p align="center">
  <img src="./assets/logo.svg" alt="handcode-tutor — learn by typing" width="900">
</p>

# handcode-tutor

> **手把手陪你练手敲代码的 AI 教练。关闭自动补全，自己敲、自己错、自己懂——AI 只在旁边讲清楚为什么。**

一个为初学者设计的 [Agent Skill](https://www.skills.sh/)，把"先核实再答 + 手把手辅导 + 协作沉淀成 howto"固化成 AI 的工作流。

---

## Why I built this

我在学编程，做了一个反潮流的选择：**关掉 IDE 的自动补全，自己敲每一个字符**。

我发现：AI 一键替我跑命令时，结果是对的、脑子是空的——**速度让我跳过了"消化"这一步**。

所以我反过来——让 AI 当老师讲清楚每个参数的意图，敲键盘的肌肉记忆留给自己。过程中会犯各种错，**但这些错恰恰是我进步的空间**。

`handcode-tutor` 把"陪练而不替手"的工作流固化下来。如果你也想把 AI 当老师，不是当手替，这个 skill 是为你写的。

---

## 它解决什么问题

你想自己敲命令学新工具（升级 lark-cli、配置 git、装 Python 包……），不想让 AI 一键搞定，也不想被 AI 一句"凭印象"的回答误导。

但用普通对话方式问 AI 时常遇到：

- **AI 瞎猜命令**：凭训练时的旧知识给你一个不存在的子命令 / 错的参数。
- **AI 替你执行**：你想自己敲找手感，AI 直接调用工具帮你跑完了。
- **学完就忘**：跑通一次就过，下次遇到类似场景从头再来。

`handcode-tutor` 把这三个坑用五条铁律封住。

---

## 五个核心价值

### 1. 学习者视角的"陪练"模式

铁律 3：**用户敲，助手解释**。除非你明确说"你来跑"，AI 只给一条命令 + 每个参数的解释 + 预期输出。你在自己的终端敲、贴回结果、AI 解读。鼓励**关闭 IDE 的自动补全**，培养代码肌肉记忆。

### 2. "先核实再答"的硬约束

铁律 1：**禁止凭训练知识库直接断言**。任何具体命令 / URL / 版本号，助手必须先：

- `<tool> --help` 看官方用法
- `npm view <pkg>` 看真实元信息
- `curl -sI <url>` 验证 URL 存在
- 读 lock 文件 / 配置文件 / 源码

查不到才答"我先查一下"——而不是一拍脑袋编出一个看起来合理的命令。

### 3. 报错按字面读

| 报错模式 | 99% 原因 |
|---|---|
| `not found matching X` | 拼写、大小写、scope 前缀 |
| `Permission denied` | 路径权限 / 该加 sudo |
| `command not found` | PATH 没配 / 没装 |
| `Module not found` | 依赖没装 / 路径错 |

诚实的报错信息是工具开发者最便宜的礼物。

### 4. 概念解释四步走

铁律 4：每个新概念第一次出现时——
1. 一句话**定义**
2. 一句话**价值**
3. 不超过 3 行的**例子**
4. **双语术语**：`英文（中文）`

不上来讲历史 / 不上来讲底层 / 不上来给大段背景。

### 5. 沉淀成可复用的 howto

跑完每次实操，AI 协助把全过程写成 `type: howto` 的 Markdown：问题清单 + 关键概念 + 完整流程 + 踩坑总结 + 下一步深入。`status: draft` 起步，**用户没说"没问题"前不算定稿**——避免 AI 一厢情愿地说"完成了"。

<p align="center">
  <img src="./assets/hero.png" alt="A learner's cyberpunk workstation — terminal demo, AI assistant explaining, howto notes distilled" width="900">
</p>

---

## 安装

```bash
# 通过 skills CLI 装到全局
npx skills add huasanai/handcode-tutor -g -y
```

装完后会在你的 agent 配置目录（Claude Code 默认是 `~/.claude/skills/`）下出现 `handcode-tutor/`。

支持的 AI agents 见 [skills.sh](https://www.skills.sh/)（Claude Code / Codex CLI / Cursor / Gemini CLI 等十几种）。

---

## 怎么唤起

在 Claude Code（或其它兼容 agent）里，说自然语言就行：

- "**我想练习手敲代码**升级一下 lark-cli"
- "陪我走完 git 配置 SSH 的流程，然后写成 howto"
- "手把手教我用 ffmpeg，我自己敲命令"
- "关闭自动补全练手感，教我用 jq"
- "边学边沉淀，给我讲清楚 npm 和 npx 的区别"

skill 会自动按"核实事实 → 手把手辅导 → 协作沉淀"三段走。

---

## 项目结构

```
handcode-tutor/
├── README.md
├── README.en.md
├── LICENSE
├── .gitignore
└── skills/
    └── handcode-tutor/
        ├── SKILL.md                       # 五条铁律 + 三阶段流程
        └── references/
            └── howto-template.md          # 沉淀文档骨架
```

---

## 设计原则

- **不替手，是陪练**。AI 不替用户敲，给指引让用户自己跑。
- **核实优先**。具体命令 / 参数 / URL 必须现场验证，不凭训练记忆作答。
- **小颗粒、能跑通**。每条命令独立给 + 参数解释 + 预期输出 + 看用户反馈决定下一步。
- **报错是对话**。把报错信息当作工具开发者的诚实回应来读，不要绕过它。
- **沉淀靠协作**。文档分 draft / stable 两态，用户没确认前永远是 draft。

---

## 支持与交流

### 联系画伞

| 平台 | 账号 |
|---|---|
| 💬 微信 | `huasanai` |
| 🐦 X | [@yfusionai](https://x.com/yfusionai) |
| 🎬 抖音 | [@画伞](https://v.douyin.com/zHu4VUhztes/) |

---

## License

MIT © 画伞 (huasan)
