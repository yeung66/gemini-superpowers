# Code Quality Reviewer Prompt Template

Use this template when reviewing code quality for a task.

**Purpose:** Verify implementation is well-built (clean, tested, maintainable)

**Only use after spec compliance review passes.**

```
## What Was Implemented

[from implementer's report]

## Plan/Requirements

Task N from [plan-file]

## Changes to Review

Base SHA: [commit before task]
HEAD SHA: [current commit]

## Review Criteria

**Code Quality:**
- Is the code clean and readable?
- Are names clear and meaningful?
- Is the structure logical?

**Testing:**
- Are tests comprehensive?
- Do tests verify actual behavior?
- Are edge cases covered?

**Best Practices:**
- Does it follow existing patterns?
- Is there any unnecessary complexity?
- Are there any potential issues?

## Report Format

**Strengths:** [what was done well]

**Issues:**
- Critical: [must fix before merge]
- Important: [should fix]
- Minor: [nice to have]

**Assessment:** Approved / Needs work
```
