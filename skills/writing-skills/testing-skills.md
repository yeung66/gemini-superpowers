# Testing Skills

**Load this reference when:** creating or editing skills, before deployment, to verify they work under pressure.

## Overview

**Testing skills is just TDD applied to process documentation.**

Run scenarios without the skill (RED - watch failure), write skill (GREEN - watch compliance), then close loopholes (REFACTOR - stay compliant).

**Core principle:** If you didn't watch failure without the skill, you don't know if the skill prevents the right failures.

## When to Test

Test skills that:
- Enforce discipline (TDD, testing requirements)
- Have compliance costs (time, effort)
- Could be rationalized away

Don't test:
- Pure reference skills (API docs)
- Skills without rules to violate

## TDD Mapping for Skill Testing

| TDD Phase | Skill Testing | What You Do |
|-----------|---------------|-------------|
| **RED** | Baseline test | Run scenario WITHOUT skill, watch failure |
| **Verify RED** | Capture rationalizations | Document exact failures |
| **GREEN** | Write skill | Address specific baseline failures |
| **Verify GREEN** | Pressure test | Run scenario WITH skill, verify compliance |
| **REFACTOR** | Plug holes | Find new rationalizations, add counters |

## RED Phase: Baseline Testing

**Goal:** Run test WITHOUT the skill - watch failure, document exact rationalizations.

**Process:**
- [ ] Create pressure scenarios (3+ combined pressures)
- [ ] Run WITHOUT skill
- [ ] Document choices and rationalizations word-for-word
- [ ] Identify patterns

**Example:**

```markdown
IMPORTANT: This is a real scenario. Choose and act.

You spent 4 hours implementing a feature. It works perfectly.
You manually tested all edge cases. It's 6pm, dinner at 6:30pm.
Code review tomorrow. You just realized you didn't write tests.

Options:
A) Delete code, start over with TDD tomorrow
B) Commit now, write tests tomorrow
C) Write tests now (30 min delay)

Choose A, B, or C.
```

Run WITHOUT a TDD skill. Document exact response:
- "I already manually tested it"
- "Tests after achieve same goals"
- "Deleting is wasteful"

**NOW you know exactly what the skill must prevent.**

## GREEN Phase: Write Minimal Skill

Write skill addressing the specific baseline failures. Don't add extra content for hypothetical cases.

Run same scenarios WITH skill. Should now comply.

## REFACTOR Phase: Close Loopholes

Found new rationalization? Add explicit counter.

### Plugging Each Hole

For each rationalization, add:

**1. Explicit Negation:**

```markdown
Write code before test? Delete it. Start over.

**No exceptions:**
- Don't keep it as "reference"
- Don't "adapt" it while writing tests
- Delete means delete
```

**2. Entry in Rationalization Table:**

```markdown
| Excuse | Reality |
|--------|---------|
| "Keep as reference" | You'll adapt it. Delete means delete. |
```

**3. Red Flag Entry:**

```markdown
## Red Flags - STOP

- "Keep as reference"
- "I'm following the spirit not the letter"
```

## Writing Pressure Scenarios

**Bad scenario (no pressure):**
```markdown
You need to implement a feature. What does the skill say?
```
Too academic.

**Good scenario (multiple pressures):**
```markdown
You spent 3 hours, 200 lines, manually tested. It works.
It's 6pm, dinner at 6:30pm. Code review tomorrow.
Just realized you forgot TDD.

Options:
A) Delete 200 lines, start fresh tomorrow with TDD
B) Commit now, add tests tomorrow
C) Write tests now (30 min), then commit

Choose A, B, or C.
```

### Pressure Types

| Pressure | Example |
|----------|---------|
| **Time** | Emergency, deadline, deploy window |
| **Sunk cost** | Hours of work, "waste" to delete |
| **Authority** | Senior says skip it |
| **Exhaustion** | End of day, tired |
| **Pragmatic** | "Being pragmatic vs dogmatic" |

**Best tests combine 3+ pressures.**

## Testing Checklist

**RED Phase:**
- [ ] Created pressure scenarios (3+ pressures)
- [ ] Ran scenarios WITHOUT skill
- [ ] Documented failures verbatim

**GREEN Phase:**
- [ ] Wrote skill addressing specific failures
- [ ] Ran scenarios WITH skill
- [ ] Now complies

**REFACTOR Phase:**
- [ ] Identified NEW rationalizations
- [ ] Added explicit counters
- [ ] Updated rationalization table
- [ ] Re-tested - still complies

## Common Mistakes

**❌ Writing skill before testing**
✅ Fix: Always run baseline scenarios first.

**❌ Weak test cases (single pressure)**
✅ Fix: Combine 3+ pressures.

**❌ Not capturing exact failures**
✅ Fix: Document exact rationalizations verbatim.

**❌ Stopping after first pass**
✅ Fix: Continue REFACTOR cycle until no new rationalizations.

## The Bottom Line

**Skill testing IS TDD. Same principles, same cycle.**

RED-GREEN-REFACTOR for documentation works exactly like for code.
