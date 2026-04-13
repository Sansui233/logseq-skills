---
name: logseq-file-journal-entry
description: Record scattered learning notes by directly reading/writing local markdown files. Use when user shares learning content or observations that should be captured in daily journal first. Works with local file system, not through Plugin API. Preferred method for recording notes.
license: MIT
---

# Logseq Journal Entry

Record scattered learning notes and observations following the journal-first workflow.

## When to Use This Skill

Use this skill when the user:
- Shares learning content, study notes, or observations
- Provides scattered knowledge points without requesting specific page maintenance
- Says things like "I learned that...", "记录一下...", "笔记..."
- Provides information that should be captured chronologically first

**Do NOT use** when:
- User explicitly asks to maintain/update a specific page or entry (use logseq-page-maintenance instead)
- User requests to add content to a specific concept page directly

## Workflow

### Step 1: Record in Today's Journal

1. Get today's date in YYYY_MM_DD format
2. Create or update `journals/YYYY_MM_DD.md`
3. Add new content using proper Logseq outline format:
   - Start with `-` for each block
   - Use TAB for indentation
   - Add `[[concept]]` links for all relevant concepts mentioned
   - Use proper Chinese formatting

Example journal entry:
```markdown
- 学习了 [[PostgreSQL]] 的架构
	- [[PostgreSQL]] 使用三层结构: database → schema → table
	- 相比 [[MySQL]] 只有两层 (database → table)
	- 这种设计提供了更好的命名空间隔离
```

### Step 2: Find Existing Pages

**IMPORTANT**: Use semantic judgment to find pages, as file names may vary.

1. List pages directory: `ls pages/ | grep -i keyword`
2. Look for similar names, variations, or related concepts
   - Example: `Postgresql.md` not `PostgreSQL.md`
   - Example: `JavaScript.md` or `JS.md` for JavaScript
3. If a potentially matching file is found, read it to confirm
4. If no matching file exists, create a new page

**Do NOT** use Grep to check aliases - this requires reading too many files.

### Step 3: Update Primary Concept Page

Only update the page if it's the PRIMARY topic of the new information.

**If page exists:**
- Read the existing page first
- Maintain existing hierarchy and formatting
- Add new information at appropriate indentation level
- Update bidirectional links

**If page doesn't exist:**
- Create new page with proper structure
- Add relevant tags: `tags:: tag1, tag2`
- Create bidirectional links to related concepts
- Use outline format with `-` and TAB indentation

### Step 4: Rely on Backlinks - Don't Duplicate

**CRITICAL PRINCIPLE**: Don't update every related page mentioned.

- Logseq's backlink feature automatically shows where a page is referenced
- Only update a page if it's the PRIMARY topic of the new information
- Secondary mentions are accessible via backlinks - no need to duplicate content

Example:
```
User: "PostgreSQL 的架构是 database → schema → table 三层结构，相比 MySQL 只有两层"

Actions:
1. Add to journals/2026_04_14.md with [[PostgreSQL]], [[MySQL]] links
2. Update Postgresql.md with architecture info (primary topic)
3. Don't update MySQL.md - it can see the reference via backlinks
```

## Logseq Format Requirements

### Outline Structure
- Every block starts with `-`
- Use TAB (not spaces) for indentation
- Headings also start with `-`: `- ## Heading`
- Ordered lists start with `-`: `- 1. item`
- Code blocks start with `-`:
  ```
  - ```javascript
    code here
    ```
  ```

### Links and Properties
- Page links: `[[页面名称]]`
- Namespace links: `[[父页面/子页面]]` (file: `父页面.子页面.md`)
- Block properties: `property:: value` (no `-` prefix)
- Page properties at top of file (no `-` prefix)

### Example Structure
```markdown
- **主题标题**
	collapse:: true
	- 详细内容
		- 子内容
			- 更深层内容
	- 相关链接: [[概念A]], [[概念B]]
- ## 章节标题
	- 章节内容
```

## File Naming Conventions

### Namespace Mapping
- File: `pages/父页面.子页面.md` → Link: `[[父页面/子页面]]`
- Use `.` (dot) in file names
- Use `/` (slash) in Logseq links

### Examples
- File: `CommonJS.Module.md` → Link: `[[CommonJS/Module]]`
- File: `JavaScript.Array.md` → Link: `[[JavaScript/Array]]`
- File: `CSS.选择器.md` → Link: `[[CSS/选择器]]`

## Quality Checks

Before finalizing:
- [ ] Journal entry created/updated with today's date
- [ ] All concepts have `[[]]` links
- [ ] Primary concept page updated (if applicable)
- [ ] Outline structure uses `-` and TAB indentation
- [ ] No duplicate content in secondary pages (rely on backlinks)
- [ ] Chinese content properly formatted
- [ ] Block properties don't start with `-`

## Common Mistakes to Avoid

1. **Don't use spaces for indentation** - Always use TAB
2. **Don't forget `-` prefix** - Every block needs it (except properties)
3. **Don't update all mentioned pages** - Only update primary topic page
4. **Don't assume exact file names** - Use semantic search and confirmation
5. **Don't skip journal entry** - Always record in journal first for this workflow

## See Also

- [Logseq Syntax Reference](references/LOGSEQ_SYNTAX.md) - Detailed syntax guide
- Use `logseq-page-maintenance` skill for direct page maintenance without journal
- Use `logseq-format-validator` skill to validate format before writing
