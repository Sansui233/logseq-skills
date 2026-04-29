---
name: logseq-file-format-validator
description: Logseq grammar guideline. Validate Logseq outlined markdown format before writing to local files. Use to check outline structure, extended markdown syntax, link syntax, property format. Works with local file system, not through Plugin API.
license: MIT
---

# Logseq Format Validator

Validate Logseq outlined markdown format to ensure proper rendering.

## When to Use This Skill

Use this skill:
- Before writing or editing any Logseq markdown file
- When user reports formatting issues or rendering problems
- To verify content follows Logseq conventions
- As a quality check before finalizing changes

**Can be used by other skills** as a validation step before file operations.

## Validation Checklist

### 1. Outline Structure

**Rule**: Every content block must start with `-`

✅ Correct:
```markdown
- Block content
	- Nested block
		- Deeper nested block
```

❌ Incorrect:
```markdown
Block content without dash
- Nested block
```

**Rule**: Use TAB for indentation, not spaces

✅ Correct:
```markdown
- Parent
	- Child (indented with TAB)
		- Grandchild (indented with TAB)
```

❌ Incorrect:
```markdown
- Parent
  - Child (indented with spaces)
    - Grandchild (indented with spaces)
```

### 2. Extended Markdown Syntax

**Rule**: Headings must start with `-`

✅ Correct:
```markdown
- ## Heading 2
	- Content under heading
- ### Heading 3
	- More content
```

❌ Incorrect:
```markdown
## Heading 2
- Content under heading
```

**Rule**: Ordered lists must start with `-`

✅ Correct:
```markdown
- 1. First item
- 2. Second item
- 3. Third item
```

❌ Incorrect:
```markdown
1. First item
2. Second item
3. Third item
```

**Rule**: Code blocks must start with `-`

✅ Correct:
```markdown
- ```javascript
	const x = 1;
	```
```

❌ Incorrect:
````markdown
```javascript
const x = 1;
```
````

### 3. Links and References

**Rule**: Use `[[]]` for page links

✅ Correct:
```markdown
- 相关概念: [[PostgreSQL]], [[MySQL]]
- 参考 [[JavaScript/Array]] 的实现
```

❌ Incorrect:
```markdown
- 相关概念: [PostgreSQL], (MySQL)
- 参考 [JavaScript/Array] 的实现
```

**Rule**: Use `(())` for block references

✅ Correct:
```markdown
- 参考上面的说明 ((block-uuid))
```

❌ Incorrect:
```markdown
- 参考上面的说明 [[block-uuid]]
```

### 4. Properties Format

**Rule**: Properties must NOT start with `-`

✅ Correct (Page properties):
```markdown
tags:: 数据库, PostgreSQL
author:: John Doe

- ## 内容开始
	- 这里才需要 dash
```

✅ Correct (Block properties):
```markdown
- **可折叠的块**
	collapse:: true
	- 块内容
```

❌ Incorrect:
```markdown
- tags:: 数据库, PostgreSQL
- author:: John Doe
```

### 5. Namespace Mapping

**Rule**: File names use `%2F` (dot), links use `/` (slash)

✅ Correct:
```markdown
File: pages/PostgreSQL%2Frole.md
Link in content: [[PostgreSQL/role]]

File: pages/JavaScript%2FArray.md
Link in content: [[JavaScript/Array]]
```

❌ Incorrect:
```markdown
File: pages/PostgreSQL/role.md
Link in content: [[PostgreSQL.role]]
```

### 6. Common Patterns

**Collapsible blocks**:
```markdown
- **标题**
	collapse:: true
	- 内容会被折叠
	- 更多内容
```

**Code blocks with language**:
```markdown
- ```javascript
	function example() {
		return true;
	}
	```
```

**Mixed content**:
```markdown
- ## 章节标题
	- 普通内容
	- **加粗内容**
		- 嵌套内容
	- ```python
		print("code")
		```
	- 1. 有序列表项
	- 2. 第二项
```

## Validation Process

### Step 1: Check Outline Structure
- [ ] Every content block starts with `-`
- [ ] Indentation uses TAB, not spaces
- [ ] Hierarchy is consistent (no skipped levels)

### Step 2: Check Extended Markdown
- [ ] Headings start with `-` (e.g., `- ## Heading`)
- [ ] Ordered lists start with `-` (e.g., `- 1. Item`)
- [ ] Code blocks start with `-` (e.g., `- ```lang`)

### Step 3: Check Links
- [ ] Page links use `[[page name]]` format
- [ ] Namespace links use `/` separator (e.g., `[[Parent/Child]]`)
- [ ] Block references use `((uuid))` format
- [ ] No broken link syntax like `[page]` or `(page)`

### Step 4: Check Properties
- [ ] Page properties at top of file (no `-` prefix)
- [ ] Block properties after block content (no `-` prefix)
- [ ] Property format: `key:: value`

### Step 5: Check Namespace Consistency
- [ ] File name uses `.` separator (e.g., `Parent.Child.md`)
- [ ] Links use `/` separator (e.g., `[[Parent/Child]]`)
- [ ] Mapping is consistent throughout file

## Common Errors and Fixes

### Error 1: Missing dash prefix
```markdown
❌ Content without dash
✅ - Content with dash
```

### Error 2: Space indentation
```markdown
❌ - Parent
  - Child (2 spaces)
✅ - Parent
	- Child (TAB)
```

### Error 3: Heading without dash
```markdown
❌ ## Heading
✅ - ## Heading
```

### Error 4: Property with dash
```markdown
❌ - tags:: value
✅ tags:: value
```

### Error 5: Wrong namespace separator
```markdown
❌ File: Parent/Child.md, Link: [[Parent.Child]]
✅ File: Parent.Child.md, Link: [[Parent/Child]]
```

### Error 6: Code block without dash
```markdown
❌ ```javascript
   code
   ```
✅ - ```javascript
	code
	```
```

## Validation Output

When validating, report:

1. **Status**: Pass/Fail
2. **Errors Found**: List specific issues with line numbers
3. **Suggested Fixes**: Concrete corrections for each error
4. **Warnings**: Non-critical issues (e.g., inconsistent spacing)

Example output:
```
❌ Validation Failed

Errors:
- Line 5: Content block missing `-` prefix
- Line 12: Heading `## Section` should be `- ## Section`
- Line 18: Property `- tags:: value` should not have `-` prefix
- Line 23: Indentation uses spaces, should use TAB

Fixes:
- Add `-` prefix to line 5
- Add `-` prefix to line 12
- Remove `-` prefix from line 18
- Replace spaces with TAB on line 23
```

## Integration with Other Skills

This skill can be called by:
- `logseq-journal-entry` - validate before writing journal entries
- `logseq-page-maintenance` - validate before updating pages
- Any workflow that writes Logseq markdown files

## Quick Reference

| Element | Format | Example |
|---------|--------|---------|
| Block | `- content` | `- 这是一个块` |
| Nested | `- parent`<br>`	- child` | Use TAB for indent |
| Heading | `- ## heading` | `- ## 章节标题` |
| Ordered list | `- 1. item` | `- 1. 第一项` |
| Code block | `- ```lang`<br>`	code`<br>`	```` | Must start with `-` |
| Page link | `[[page]]` | `[[PostgreSQL]]` |
| Namespace link | `[[parent/child]]` | `[[PostgreSQL/role]]` |
| Block ref | `((uuid))` | `((abc-123))` |
| Page property | `key:: value` | `tags:: 数据库` |
| Block property | After block, no `-` | `collapse:: true` |
| File name | `Parent.Child.md` | Use `.` separator |

## See Also

- [Logseq Syntax Reference](references/LOGSEQ_SYNTAX.md) - Complete syntax guide
- [Quality Checklist](references/QUALITY_CHECKLIST.md) - Full quality checks
