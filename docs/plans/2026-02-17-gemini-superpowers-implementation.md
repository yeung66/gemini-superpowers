# Gemini Superpowers Implementation Plan

> **For Gemini:** 使用此计划逐任务实现 gemini-superpowers 项目。

**Goal:** 将 obra/superpowers 的 14 个 skills 完整适配为 Gemini CLI 可用格式。

**Architecture:** 从原始 superpowers 项目读取每个 skill，按照工具映射规则进行适配，写入到新项目的 skills 目录中。

**Tech Stack:** Markdown, Git, Gemini CLI skills format

---

## Task 1: 创建项目基础文件

**Files:**
- Create: `README.md`
- Create: `LICENSE`

**Step 1: 创建 README.md**

创建项目说明文件，包含安装指南和 skills 列表。

**Step 2: 创建 LICENSE**

创建 MIT 许可证文件。

**Step 3: Commit**

```bash
git add README.md LICENSE
git commit -m "docs: add README and LICENSE"
```

---

## Task 2: 适配 using-gemini-superpowers skill

**Files:**
- Create: `skills/using-gemini-superpowers/SKILL.md`

**Source:** `superpowers/skills/using-superpowers/SKILL.md`

**适配要点:**
- 重命名为 `using-gemini-superpowers`
- 将 `Skill` tool 引用改为直接 skill 名称引用
- 将 `superpowers:skill-name` 改为 `skill-name`
- 将 `CLAUDE.md` 改为 `GEMINI.md`
- 删除 Claude Code 特有的工具调用语法

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/using-gemini-superpowers/SKILL.md
git commit -m "feat: add using-gemini-superpowers skill"
```

---

## Task 3: 适配 brainstorming skill

**Files:**
- Create: `skills/brainstorming/SKILL.md`

**Source:** `superpowers/skills/brainstorming/SKILL.md`

**适配要点:**
- 将 `TodoWrite` 改为 `write_todos`
- 将 `superpowers:writing-plans` 改为 `writing-plans`
- 将 `your human partner` 改为 `the user`

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/brainstorming/SKILL.md
git commit -m "feat: add brainstorming skill"
```

---

## Task 4: 适配 test-driven-development skill

**Files:**
- Create: `skills/test-driven-development/SKILL.md`
- Create: `skills/test-driven-development/testing-anti-patterns.md`

**Source:** `superpowers/skills/test-driven-development/`

**适配要点:**
- 将 `your human partner` 改为 `the user`
- 保持大部分内容不变（方法论为主）

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/test-driven-development/
git commit -m "feat: add test-driven-development skill"
```

---

## Task 5: 适配 systematic-debugging skill

**Files:**
- Create: `skills/systematic-debugging/SKILL.md`
- Create: `skills/systematic-debugging/condition-based-waiting.md`
- Create: `skills/systematic-debugging/defense-in-depth.md`
- Create: `skills/systematic-debugging/root-cause-tracing.md`

**Source:** `superpowers/skills/systematic-debugging/`

**适配要点:**
- 将 `your human partner` 改为 `the user`
- 将 `superpowers:test-driven-development` 改为 `test-driven-development`
- 将 `superpowers:verification-before-completion` 改为 `verification-before-completion`

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/systematic-debugging/
git commit -m "feat: add systematic-debugging skill"
```

---

## Task 6: 适配 writing-plans skill

**Files:**
- Create: `skills/writing-plans/SKILL.md`

**Source:** `superpowers/skills/writing-plans/SKILL.md`

**适配要点:**
- 将 `TodoWrite` 改为 `write_todos`
- 将 `superpowers:executing-plans` 改为 `executing-plans`
- 将 `superpowers:subagent-driven-development` 改为 `subagent-driven-development`

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/writing-plans/SKILL.md
git commit -m "feat: add writing-plans skill"
```

---

## Task 7: 适配 executing-plans skill

**Files:**
- Create: `skills/executing-plans/SKILL.md`

**Source:** `superpowers/skills/executing-plans/SKILL.md`

**适配要点:**
- 将 `TodoWrite` 改为 `write_todos`
- 将 `superpowers:finishing-a-development-branch` 改为 `finishing-a-development-branch`
- 将 `superpowers:using-git-worktrees` 改为 `using-git-worktrees`
- 将 `your human partner` 改为 `the user`

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/executing-plans/SKILL.md
git commit -m "feat: add executing-plans skill"
```

---

## Task 8: 适配 subagent-driven-development skill

**Files:**
- Create: `skills/subagent-driven-development/SKILL.md`
- Create: `skills/subagent-driven-development/implementer-prompt.md`
- Create: `skills/subagent-driven-development/spec-reviewer-prompt.md`
- Create: `skills/subagent-driven-development/code-quality-reviewer-prompt.md`

**Source:** `superpowers/skills/subagent-driven-development/`

**适配要点:**
- 将 `Task` tool 概念改为"分步执行"流程描述
- 将 `TodoWrite` 改为 `write_todos`
- 将所有 `superpowers:*` 引用去掉前缀
- 将 "subagent" 概念改为"分步处理"或保留但解释为通用概念

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/subagent-driven-development/
git commit -m "feat: add subagent-driven-development skill"
```

---

## Task 9: 适配 dispatching-parallel-agents skill

**Files:**
- Create: `skills/dispatching-parallel-agents/SKILL.md`

**Source:** `superpowers/skills/dispatching-parallel-agents/SKILL.md`

**适配要点:**
- 将 `Task()` 调用改为通用流程描述
- 保持并行处理的概念

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/dispatching-parallel-agents/SKILL.md
git commit -m "feat: add dispatching-parallel-agents skill"
```

---

## Task 10: 适配 using-git-worktrees skill

**Files:**
- Create: `skills/using-git-worktrees/SKILL.md`

**Source:** `superpowers/skills/using-git-worktrees/SKILL.md`

**适配要点:**
- 将 `CLAUDE.md` 改为 `GEMINI.md`
- 将所有 `superpowers:*` 引用去掉前缀

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/using-git-worktrees/SKILL.md
git commit -m "feat: add using-git-worktrees skill"
```

---

## Task 11: 适配 finishing-a-development-branch skill

**Files:**
- Create: `skills/finishing-a-development-branch/SKILL.md`

**Source:** `superpowers/skills/finishing-a-development-branch/SKILL.md`

**适配要点:**
- 将所有 `superpowers:*` 引用去掉前缀

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/finishing-a-development-branch/SKILL.md
git commit -m "feat: add finishing-a-development-branch skill"
```

---

## Task 12: 适配 requesting-code-review skill

**Files:**
- Create: `skills/requesting-code-review/SKILL.md`
- Create: `skills/requesting-code-review/code-reviewer.md`

**Source:** `superpowers/skills/requesting-code-review/`

**适配要点:**
- 将 `Task` tool 概念改为通用流程
- 将 `superpowers:code-reviewer` 改为 `code-reviewer`

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/requesting-code-review/
git commit -m "feat: add requesting-code-review skill"
```

---

## Task 13: 适配 receiving-code-review skill

**Files:**
- Create: `skills/receiving-code-review/SKILL.md`

**Source:** `superpowers/skills/receiving-code-review/SKILL.md`

**适配要点:**
- 将 `your human partner` 改为 `the user`
- 将 `CLAUDE.md` 改为 `GEMINI.md`（如有）

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/receiving-code-review/SKILL.md
git commit -m "feat: add receiving-code-review skill"
```

---

## Task 14: 适配 verification-before-completion skill

**Files:**
- Create: `skills/verification-before-completion/SKILL.md`

**Source:** `superpowers/skills/verification-before-completion/SKILL.md`

**适配要点:**
- 将 `your human partner` 改为 `the user`
- 将 "Agent" 术语改为通用描述或删除

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/verification-before-completion/SKILL.md
git commit -m "feat: add verification-before-completion skill"
```

---

## Task 15: 适配 writing-skills skill

**Files:**
- Create: `skills/writing-skills/SKILL.md`
- Create: `skills/writing-skills/anthropic-best-practices.md`
- Create: `skills/writing-skills/persuasion-principles.md`
- Create: `skills/writing-skills/testing-skills-with-subagents.md`

**Source:** `superpowers/skills/writing-skills/`

**适配要点:**
- 将 `~/.claude/skills` 改为 `~/.gemini/skills`
- 将 `superpowers:*` 引用去掉前缀
- 将 `TodoWrite` 改为 `write_todos`
- 将 "anthropic-best-practices" 内容更新为通用最佳实践

**Step 1: 读取原始文件并适配**

**Step 2: 写入新文件**

**Step 3: Commit**

```bash
git add skills/writing-skills/
git commit -m "feat: add writing-skills skill"
```

---

## Task 16: 最终验证和清理

**Step 1: 验证目录结构**

```bash
find skills -name "*.md" | sort
```

确认所有 14 个 skills 都已创建。

**Step 2: 验证 SKILL.md 格式**

检查每个 SKILL.md 都有正确的 YAML frontmatter（name 和 description）。

**Step 3: 最终 commit**

```bash
git add -A
git commit -m "chore: final cleanup and verification"
```

---

## 完成标准

- [ ] 14 个 skills 全部创建
- [ ] 所有 SKILL.md 有正确的 YAML frontmatter
- [ ] 所有 Claude Code 特有语法已替换
- [ ] README.md 包含安装指南
- [ ] LICENSE 文件存在
- [ ] 所有文件已提交到 git
