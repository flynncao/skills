<a id="chinese-guide"></a>

# Flynn 的自用 Skills 仓库

[English](README.en.md#english-guide)

---

## 项目简介

这是我的自用 AI Skills 仓库，用来集中维护我在日常开发里会反复使用的 Skills。

这些 Skills 的目标很直接：

- 把高频但容易重复说明的工作流程沉淀成可复用能力
- 让 Codex、Claude Code 或兼容客户端在合适场景下自动调用对应 Skill
- 降低我在不同设备、不同客户端之间迁移 Skills 的成本

当前仓库中的 Skill 会持续增加；你可以安装整个仓库，也可以只安装其中某一个 Skill。

## 安装

### 方法一：通过 npx 一键安装（推荐）

```bash
npx skills add https://github.com/flynncao/skills --skills commit-with-agent
```

这是最直接的安装方式，会把指定 Skill 安装到正确的 Skills 目录中。

如果后续仓库里新增了其他 Skill，也可以继续用同样的方式按名字安装。

### 方法二：通过 Git 克隆整个仓库

```bash
git clone https://github.com/flynncao/skills.git
```

克隆后，你可以按需把某个 Skill 目录复制到自己的客户端 Skills 目录中。

### 方法三：手动安装

1. 下载本仓库 ZIP，或先执行 `git clone`
2. 选择你需要的 Skill 目录，例如 `commit-with-agent`
3. 将该目录复制到你的客户端 Skills 目录

常见目录如下：

- Codex
  - macOS / Linux: `~/.codex/skills/`
  - Windows: `%USERPROFILE%\\.codex\\skills\\`
- Claude Code
  - macOS / Linux: `~/.claude/skills/`
  - Windows: `%USERPROFILE%\\.claude\\skills\\`

例如把 `commit-with-agent` 安装到 Codex：

```bash
cp -R commit-with-agent ~/.codex/skills/
```

Windows 可以直接把文件夹复制到：

```text
%USERPROFILE%\.codex\skills\commit-with-agent\
```

### 目录结构示例

安装后的结构建议保持完整，例如：

```text
~/.codex/skills/commit-with-agent/
├── SKILL.md
├── README.md
├── README.en.md
└── references/
```

如果缺少 `references/` 或说明文件，某些 Skill 可能无法按预期工作。

### 验证安装

安装完成后，重启客户端或重新加载 Skills，然后在对话中直接描述需求，或者显式提到 Skill 名称。

以 `commit-with-agent` 为例，你可以直接说：

```text
把现在的修改提交，并且以 codex 和 claude 作为协作者
```

如果客户端正确识别并触发 Skill，说明安装已经生效。

## 使用

### 基础用法

本仓库中的 Skill 以自然语言触发为主。大多数情况下，你不需要记额外命令，只需要把目标说清楚。

常见方式有三种：

#### 1. 直接描述需求

```text
把现在的修改提交，并带上 AI 协作者
```

#### 2. 显式点名某个 Skill

```text
使用 commit-with-agent 帮我提交这次改动
```

#### 3. 进入单个 Skill 查看专用说明

每个 Skill 目录通常都带有自己的 README，你可以在那里看：

- 它解决什么问题
- 推荐怎么说
- 它会产出什么结果

## 当前收录的 Skills

### `commit-with-agent`

路径：[`commit-with-agent`](commit-with-agent/)

用途：

- 在保留原有提交流程的前提下，为提交信息追加 AI 协作者尾注
- 支持 `Codex`、`Claude` 等 `Co-authored-by` 署名
- 适合希望在 Git 历史中保留 AI 协作归因的场景

安装示例：

```bash
npx skills add https://github.com/flynncao/skills --skills commit-with-agent
```

## 文件说明

- `README.md`：中文总览与安装使用指南
- `README.en.md`：英文总览与安装使用指南
- `README_refernece.md`：本次 README 改写参考文档
- `*/SKILL.md`：单个 Skill 的定义文件
- `*/README.md`：单个 Skill 的中文说明
- `*/README.en.md`：单个 Skill 的英文说明
- `*/references/`：单个 Skill 依赖的补充说明或模板

---
