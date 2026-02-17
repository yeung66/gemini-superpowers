# Persuasion Principles for Skill Design

## Overview

LLMs respond to the same persuasion principles as humans. Understanding this helps design effective skills - not to manipulate, but to ensure critical practices are followed.

**Research foundation:** Meincke et al. (2025) tested persuasion principles with N=28,000 AI conversations. Compliance rates more than doubled with persuasion techniques.

## The Key Principles

### 1. Authority
**What it is:** Deference to expertise, credentials, or official sources.

**How it works in skills:**
- Imperative language: "YOU MUST", "Never", "Always"
- Non-negotiable framing: "No exceptions"
- Eliminates rationalization

**When to use:**
- Discipline-enforcing skills (TDD, verification requirements)
- Safety-critical practices

**Example:**
```markdown
✅ Write code before test? Delete it. Start over. No exceptions.
❌ Consider writing tests first when feasible.
```

### 2. Commitment
**What it is:** Consistency with prior actions or statements.

**How it works in skills:**
- Require announcements: "Announce skill usage"
- Force explicit choices: "Choose A, B, or C"
- Use tracking: Task lists for checklists

**When to use:**
- Ensuring skills are actually followed
- Multi-step processes

### 3. Scarcity
**What it is:** Urgency from time limits.

**How it works in skills:**
- Time-bound requirements: "Before proceeding"
- Sequential dependencies: "Immediately after X"

**When to use:**
- Immediate verification requirements
- Preventing "I'll do it later"

### 4. Social Proof
**What it is:** Conformity to what others do.

**How it works in skills:**
- Universal patterns: "Every time", "Always"
- Failure modes: "X without Y = failure"

**When to use:**
- Documenting universal practices
- Warning about common failures

### 5. Unity
**What it is:** Shared identity, "we-ness".

**How it works in skills:**
- Collaborative language: "our codebase", "we're colleagues"
- Shared goals

**When to use:**
- Collaborative workflows
- Non-hierarchical practices

## Principle Combinations by Skill Type

| Skill Type | Use | Avoid |
|------------|-----|-------|
| Discipline-enforcing | Authority + Commitment + Social Proof | Liking, Reciprocity |
| Guidance/technique | Moderate Authority + Unity | Heavy authority |
| Collaborative | Unity + Commitment | Authority |
| Reference | Clarity only | All persuasion |

## Why This Works

**Bright-line rules reduce rationalization:**
- "YOU MUST" removes decision fatigue
- Absolute language eliminates "is this an exception?" questions

**Implementation intentions create automatic behavior:**
- Clear triggers + required actions = automatic execution
- "When X, do Y" more effective than "generally do Y"

## Ethical Use

**Legitimate:**
- Ensuring critical practices are followed
- Creating effective documentation
- Preventing predictable failures

**The test:** Would this technique serve the user's genuine interests if they fully understood it?

## Research Citations

**Cialdini, R. B. (2021).** *Influence: The Psychology of Persuasion.* Harper Business.

**Meincke, L., et al. (2025).** Call Me A Jerk: Persuading AI to Comply. University of Pennsylvania.

## Quick Reference

When designing a skill, ask:

1. **What type is it?** (Discipline vs. guidance vs. reference)
2. **What behavior am I trying to change?**
3. **Which principle(s) apply?**
4. **Is this ethical?** (Serves user's genuine interests?)
