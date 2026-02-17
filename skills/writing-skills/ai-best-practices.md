# Skill Authoring Best Practices

Good Skills are concise, well-structured, and tested with real usage.

## Core Principles

### Concise is Key

The context window is a public good. Your Skill shares it with everything else:

* The system prompt
* Conversation history
* Other Skills' metadata
* Your actual request

**Default assumption**: The AI is already very smart

Only add context it doesn't already have. Challenge each piece of information:

* "Does it really need this explanation?"
* "Can I assume it knows this?"
* "Does this paragraph justify its token cost?"

**Good example: Concise** (approximately 50 tokens):

````markdown
## Extract PDF text

Use pdfplumber for text extraction:

```python
import pdfplumber

with pdfplumber.open("file.pdf") as pdf:
    text = pdf.pages[0].extract_text()
```
````

**Bad example: Too verbose** (approximately 150 tokens):

```markdown
## Extract PDF text

PDF (Portable Document Format) files are a common file format that contains
text, images, and other content. To extract text from a PDF, you'll need to
use a library...
```

### Target Word Counts

- Frequently-loaded skills: <200 words
- Other skills: <500 words (still be concise)

### Move Details to References

```markdown
# ❌ BAD: Document all flags
search-conversations supports --text, --both, --after DATE...

# ✅ GOOD: Reference help
search-conversations supports multiple modes. Run --help for details.
```

## Structure

### Required Elements

1. **Frontmatter** - name and description (max 1024 chars total)
2. **Overview** - Core principle in 1-2 sentences
3. **When to Use** - Triggering conditions

### Optional Elements

- Quick reference table
- Code examples
- Common mistakes
- Supporting files

## Description Field

**Format:** Start with "Use when..." describing triggering conditions only.

**NEVER** summarize the skill's process in the description. This causes the AI to follow the description instead of reading the full skill.

```yaml
# ❌ BAD: Summarizes workflow
description: Execute plans task by task with code review between each

# ✅ GOOD: Just triggers
description: Use when executing implementation plans with independent tasks
```

## Code Examples

Provide one excellent, runnable example rather than multiple mediocre ones:

```python
# ✅ GOOD: Complete, runnable, well-commented
import pdfplumber

with pdfplumber.open("document.pdf") as pdf:
    # Extract text from first page
    text = pdf.pages[0].extract_text()
    print(text)
```

## Testing Skills

Before deploying:

1. **Baseline test** - Run scenario WITHOUT skill, document failures
2. **Pressure test** - Run WITH skill under realistic pressure
3. **Refactor** - Close any loopholes found

## Checklist

- [ ] Name uses only letters, numbers, hyphens
- [ ] Description starts with "Use when..."
- [ ] Description under 500 characters
- [ ] Overview has core principle
- [ ] Tested with realistic scenarios
- [ ] One excellent example (not multi-language)
