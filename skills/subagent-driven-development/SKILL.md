---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# Subagent-Driven Development

Execute plan by processing tasks one by one with fresh context, with two-stage review after each: spec compliance review first, then code quality review.

**Core principle:** Fresh context per task + two-stage review (spec then quality) = high quality, fast iteration

## When to Use

```dot
digraph when_to_use {
    "Have implementation plan?" [shape=diamond];
    "Tasks mostly independent?" [shape=diamond];
    "Stay in this session?" [shape=diamond];
    "subagent-driven-development" [shape=box];
    "executing-plans" [shape=box];
    "Manual execution or brainstorm first" [shape=box];

    "Have implementation plan?" -> "Tasks mostly independent?" [label="yes"];
    "Have implementation plan?" -> "Manual execution or brainstorm first" [label="no"];
    "Tasks mostly independent?" -> "Stay in this session?" [label="yes"];
    "Tasks mostly independent?" -> "Manual execution or brainstorm first" [label="no - tightly coupled"];
    "Stay in this session?" -> "subagent-driven-development" [label="yes"];
    "Stay in this session?" -> "executing-plans" [label="no - parallel session"];
}
```

**vs. Executing Plans (parallel session):**
- Same session (no context switch)
- Fresh context per task (no context pollution)
- Two-stage review after each task: spec compliance first, then code quality
- Faster iteration (no human-in-loop between tasks)

## The Process

```dot
digraph process {
    rankdir=TB;

    subgraph cluster_per_task {
        label="Per Task";
        "Start implementation (./implementer-prompt.md)" [shape=box];
        "Questions about task?" [shape=diamond];
        "Answer questions, provide context" [shape=box];
        "Implement, test, commit, self-review" [shape=box];
        "Spec compliance review (./spec-reviewer-prompt.md)" [shape=box];
        "Code matches spec?" [shape=diamond];
        "Fix spec gaps" [shape=box];
        "Code quality review (./code-quality-reviewer-prompt.md)" [shape=box];
        "Quality approved?" [shape=diamond];
        "Fix quality issues" [shape=box];
        "Mark task complete" [shape=box];
    }

    "Read plan, extract all tasks with full text, note context, create task list" [shape=box];
    "More tasks remain?" [shape=diamond];
    "Final code review for entire implementation" [shape=box];
    "Use finishing-a-development-branch" [shape=box style=filled fillcolor=lightgreen];

    "Read plan, extract all tasks with full text, note context, create task list" -> "Start implementation (./implementer-prompt.md)";
    "Start implementation (./implementer-prompt.md)" -> "Questions about task?";
    "Questions about task?" -> "Answer questions, provide context" [label="yes"];
    "Answer questions, provide context" -> "Start implementation (./implementer-prompt.md)";
    "Questions about task?" -> "Implement, test, commit, self-review" [label="no"];
    "Implement, test, commit, self-review" -> "Spec compliance review (./spec-reviewer-prompt.md)";
    "Spec compliance review (./spec-reviewer-prompt.md)" -> "Code matches spec?";
    "Code matches spec?" -> "Fix spec gaps" [label="no"];
    "Fix spec gaps" -> "Spec compliance review (./spec-reviewer-prompt.md)" [label="re-review"];
    "Code matches spec?" -> "Code quality review (./code-quality-reviewer-prompt.md)" [label="yes"];
    "Code quality review (./code-quality-reviewer-prompt.md)" -> "Quality approved?";
    "Quality approved?" -> "Fix quality issues" [label="no"];
    "Fix quality issues" -> "Code quality review (./code-quality-reviewer-prompt.md)" [label="re-review"];
    "Quality approved?" -> "Mark task complete" [label="yes"];
    "Mark task complete" -> "More tasks remain?";
    "More tasks remain?" -> "Start implementation (./implementer-prompt.md)" [label="yes"];
    "More tasks remain?" -> "Final code review for entire implementation" [label="no"];
    "Final code review for entire implementation" -> "Use finishing-a-development-branch";
}
```

## Prompt Templates

- `./implementer-prompt.md` - Implementation guidance
- `./spec-reviewer-prompt.md` - Spec compliance review guidance
- `./code-quality-reviewer-prompt.md` - Code quality review guidance

## Example Workflow

```
You: I'm using Subagent-Driven Development to execute this plan.

[Read plan file once: docs/plans/feature-plan.md]
[Extract all 5 tasks with full text and context]
[Create task list with all tasks]

Task 1: Hook installation script

[Get Task 1 text and context (already extracted)]
[Start implementation with full task text + context]

Question: "Before I begin - should the hook be installed at user or system level?"

Answer: "User level (~/.config/superpowers/hooks/)"

Implementation:
  - Implemented install-hook command
  - Added tests, 5/5 passing
  - Self-review: Found I missed --force flag, added it
  - Committed

[Spec compliance review]
Spec reviewer: ✅ Spec compliant - all requirements met, nothing extra

[Code quality review]
Code reviewer: Strengths: Good test coverage, clean. Issues: None. Approved.

[Mark Task 1 complete]

Task 2: Recovery modes

[Get Task 2 text and context (already extracted)]
[Start implementation with full task text + context]

[No questions, proceeds]
Implementation:
  - Added verify/repair modes
  - 8/8 tests passing
  - Self-review: All good
  - Committed

[Spec compliance review]
Spec reviewer: ❌ Issues:
  - Missing: Progress reporting (spec says "report every 100 items")
  - Extra: Added --json flag (not requested)

[Fix issues]
Implementer: Removed --json flag, added progress reporting

[Spec reviewer reviews again]
Spec reviewer: ✅ Spec compliant now

[Code quality review]
Code reviewer: Strengths: Solid. Issues (Important): Magic number (100)

[Fix]
Implementer: Extracted PROGRESS_INTERVAL constant

[Code reviewer reviews again]
Code reviewer: ✅ Approved

[Mark Task 2 complete]

...

[After all tasks]
[Final code review]
Final reviewer: All requirements met, ready to merge

Done!
```

## Advantages

**vs. Manual execution:**
- Follow TDD naturally
- Fresh context per task (no confusion)
- Can ask questions (before AND during work)

**vs. Executing Plans:**
- Same session (no handoff)
- Continuous progress (no waiting)
- Review checkpoints automatic

**Quality gates:**
- Self-review catches issues before handoff
- Two-stage review: spec compliance, then code quality
- Review loops ensure fixes actually work
- Spec compliance prevents over/under-building
- Code quality ensures implementation is well-built

## Red Flags

**Never:**
- Start implementation on main/master branch without explicit user consent
- Skip reviews (spec compliance OR code quality)
- Proceed with unfixed issues
- Provide full task text (don't make implementer read plan file)
- Skip scene-setting context (implementer needs to understand where task fits)
- Ignore questions (answer before letting them proceed)
- Accept "close enough" on spec compliance (spec reviewer found issues = not done)
- Skip review loops (reviewer found issues = fix = review again)
- Let self-review replace actual review (both are needed)
- **Start code quality review before spec compliance is ✅** (wrong order)
- Move to next task while either review has open issues

**If questions arise:**
- Answer clearly and completely
- Provide additional context if needed
- Don't rush into implementation

**If reviewer finds issues:**
- Fix them
- Review again
- Repeat until approved
- Don't skip the re-review

## Integration

**Required workflow skills:**
- **using-git-worktrees** - REQUIRED: Set up isolated workspace before starting
- **writing-plans** - Creates the plan this skill executes
- **requesting-code-review** - Code review template for reviewer steps
- **finishing-a-development-branch** - Complete development after all tasks

**Should use:**
- **test-driven-development** - Follow TDD for each task

**Alternative workflow:**
- **executing-plans** - Use for parallel session instead of same-session execution
