# Gemini Superpowers 设计文档

## 概述

将 [obra/superpowers](https://github.com/obra/superpowers) 项目的 skills 适配为 Gemini CLI 可用的格式，使用户可以通过 Gemini CLI 原生命令安装这些 skills。

## 目标

- 完整移植 14 个 skills 到 Gemini CLI
- 使用 Gemini CLI 原生安装方式：`gemini skills install https://github.com/用户名/gemini-superpowers.git`
- 完全适配所有 Claude Code 特有语法为 Gemini CLI 等效方式

## 工具映射规则

### 工具名称映射

| Claude Code | Gemini CLI | 处理方式 |
|-------------|------------|----------|
| `Task` (subagent dispatch) | 流程描述 | 改为"分步执行"或"按任务逐个处理" |
| `TaskCreate/TaskUpdate/TaskList/TaskGet` | `write_todos` | 直接替换 |
| `TodoWrite` | `write_todos` | 直接替换 |
| `Skill` tool | `@skill-name` 或直接引用 | 使用 Gemini 语法 |
| `Read` | `ReadFile` | 直接替换 |
| `Edit` | `Edit` | 保持不变 |
| `Write` | `WriteFile` | 直接替换 |
| `Bash` | `Shell` | 直接替换 |
| `Glob` | `FindFiles` | 直接替换 |
| `Grep` | `SearchText` | 直接替换 |
| `WebFetch` | `WebFetch` | 保持不变 |
| `WebSearch` | `GoogleSearch` | 直接替换 |
| `AskUserQuestion` | `ask_user` | 直接替换 |

### 术语映射

| Claude Code | Gemini CLI |
|-------------|------------|
| `your human partner` | `the user` |
| `CLAUDE.md` | `GEMINI.md` |
| `~/.claude/skills` | `~/.gemini/skills` |
| `superpowers:skill-name` | `skill-name` (去掉前缀) |

### 跳过的内容

- `code-reviewer` subagent 类型 → 改为通用流程描述
- Claude Code 特有的 hooks 系统 → 简化或跳过

## 项目结构

```
gemini-superpowers/
├── README.md
├── LICENSE
├── skills/
│   ├── brainstorming/
│   │   └── SKILL.md
│   ├── test-driven-development/
│   │   ├── SKILL.md
│   │   └── testing-anti-patterns.md
│   ├── systematic-debugging/
│   │   ├── SKILL.md
│   │   ├── condition-based-waiting.md
│   │   ├── defense-in-depth.md
│   │   └── root-cause-tracing.md
│   ├── writing-plans/
│   │   └── SKILL.md
│   ├── executing-plans/
│   │   └── SKILL.md
│   ├── subagent-driven-development/
│   │   ├── SKILL.md
│   │   ├── implementer-prompt.md
│   │   ├── spec-reviewer-prompt.md
│   │   └── code-quality-reviewer-prompt.md
│   ├── dispatching-parallel-agents/
│   │   └── SKILL.md
│   ├── using-git-worktrees/
│   │   └── SKILL.md
│   ├── finishing-a-development-branch/
│   │   └── SKILL.md
│   ├── requesting-code-review/
│   │   ├── SKILL.md
│   │   └── code-reviewer.md
│   ├── receiving-code-review/
│   │   └── SKILL.md
│   ├── verification-before-completion/
│   │   └── SKILL.md
│   ├── using-gemini-superpowers/
│   │   └── SKILL.md
│   └── writing-skills/
│       ├── SKILL.md
│       ├── anthropic-best-practices.md
│       ├── persuasion-principles.md
│       └── testing-skills-with-subagents.md
```

## Skills 列表

| Skill | 用途 |
|-------|------|
| `brainstorming` | 将想法转化为完整设计 |
| `test-driven-development` | TDD 方法论 - RED-GREEN-REFACTOR |
| `systematic-debugging` | 系统化调试 - 4阶段根因分析 |
| `writing-plans` | 编写详细实现计划 |
| `executing-plans` | 批量执行计划 |
| `subagent-driven-development` | 分步执行计划，每任务独立处理 |
| `dispatching-parallel-agents` | 并行处理独立任务 |
| `using-git-worktrees` | Git worktree 隔离工作区 |
| `finishing-a-development-branch` | 完成分支工作 |
| `requesting-code-review` | 请求代码审查 |
| `receiving-code-review` | 接收代码审查反馈 |
| `verification-before-completion` | 完成前验证 |
| `using-gemini-superpowers` | 框架入门（重命名） |
| `writing-skills` | 创建新 skills |

## 安装方式

```bash
gemini skills install https://github.com/用户名/gemini-superpowers.git
```

## 适配原则

1. **方法论优先**：大部分 skills 是方法论指导，工具调用只是示例
2. **等效替换**：Claude Code 工具替换为 Gemini CLI 等效工具
3. **通用化**：将平台特定术语改为通用描述
4. **保持结构**：保留原始 skill 的目录结构和辅助文件

## 致谢

本项目基于 [obra/superpowers](https://github.com/obra/superpowers) 改编。
