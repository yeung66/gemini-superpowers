# Gemini Superpowers

AI 驱动的软件开发工作流框架，为 Gemini CLI 提供可组合的 "skills"，自动引导 AI 遵循最佳实践。

> 本项目改编自 [obra/superpowers](https://github.com/obra/superpowers)，针对 Gemini CLI 进行了完整适配。

## 安装

```bash
gemini skills install https://github.com/你的用户名/gemini-superpowers.git
```

## 核心工作流（7 步流程）

1. **Brainstorming** — 通过问答细化想法，逐步呈现设计
2. **Using Git Worktrees** — 创建隔离的开发分支
3. **Writing Plans** — 将任务拆分为 2-5 分钟的小步骤
4. **Executing Plans** — 批量执行计划，带检查点
5. **Test-Driven Development** — 强制 RED-GREEN-REFACTOR 循环
6. **Code Review** — 基于严重程度的问题报告
7. **Finishing Branch** — 验证测试、合并/PR、清理工作区

## Skills 列表

| Skill | 用途 |
|-------|------|
| `brainstorming` | 将想法转化为完整设计 |
| `test-driven-development` | TDD 方法论 |
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
| `using-gemini-superpowers` | 框架入门 |
| `writing-skills` | 创建新 skills |

## 使用方式

安装后，Gemini CLI 会根据你的任务自动激活相关 skill。

你也可以直接引用：
```
请使用 brainstorming skill 帮我设计这个功能
```

## 设计哲学

- 测试驱动开发作为强制实践
- 系统化流程优于临时方案
- 简洁是首要设计目标
- 基于证据的验证，而非假设

## 致谢

本项目基于 [obra/superpowers](https://github.com/obra/superpowers) 改编，感谢原作者的出色工作。

## 许可证

MIT
