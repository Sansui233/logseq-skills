---
name: logseq-file-page-maintenance
description: Maintain Logseq wiki entries by directly reading/writing local markdown files. Use when user explicitly requests to update a specific page. Works with local file system, not through Plugin API. Preferred method for daily maintenance workflow.
license: MIT
---

# Logseq Page Maintenance

Directly maintain and update specific wiki entries, bypassing the journal workflow.

## When to Use This Skill

Use this skill when the user:
- Explicitly asks to maintain or update a specific page/entry
- Requests to add a concept page or namespace child page
- Says things like "给 X 词条增加...", "更新 X 页面...", "创建 [[X/Y]] 页面"
- Wants to work directly on structured wiki content

**Do NOT use** when:
- User shares scattered learning notes or observations (use logseq-journal-entry instead)
- User provides information without specifying a target page

## Workflow

### Step 1: Find Existing Pages

**IMPORTANT**: Use semantic judgment to find pages, as file names may vary.

1. List pages directory: `ls pages/ | grep -i keyword`
2. Look for similar names, variations, or related concepts. Consider for both Chinese and English keywords.
   - Example: `Postgresql.md` or `PostgreSQL.md`
   - Example: `JavaScript.md` or `JS.md` for JavaScript
   - Example: `Animation.md` or `动画.md`
3. If a potentially matching file is found, read it to confirm
4. If no matching file exists, proceed to create the page

**Do NOT** use Grep to check aliases - this requires reading too many files.

### Step 2: Create or Update Target Page

**For Regular Pages:**

If page exists:
- Read the existing page first
- Maintain existing hierarchy and formatting
- Add new information at appropriate indentation level
- Update bidirectional links

If page doesn't exist:
- Create new page with proper structure. The page name should follow wiki name atomic convention.
- Add relevant tags: `tags:: tag1, tag2`
- Create bidirectional links to related concepts
- Use outline format with `-` and TAB indentation

### Step 3: Update Parent Page Index (for namespace children)

When creating a namespace child page (e.g., `[[Parent/Child]]`):

1. Find and read the parent page (e.g., `Parent.md`)
2. Add reference to the new child page in appropriate section
3. Maintain parent page's structure and hierarchy
4. Use proper outline format

Example:
```markdown
- ## 相关概念
	- [[PostgreSQL/role]] - 角色和权限管理
	- [[PostgreSQL/schema]] - 模式和命名空间
```

### Step 4: No Journal Entry Needed

**CRITICAL**: This workflow skips journal creation entirely.

- Do NOT create or update journal entries
- Work directly on the target page
- This is for structured wiki maintenance, not chronological recording

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
- Namespace links: `[[父页面/子页面]]` (file: `父页面%2F子页面.md`)
- Block properties: `property:: value` (no `-` prefix)
- Page properties at top of file (no `-` prefix)

### Example Structure
```markdown
tags:: 数据库, PostgreSQL

- ## 概述
	- [[PostgreSQL]] 的角色系统用于管理权限
	- 相关概念: [[PostgreSQL/schema]], [[PostgreSQL/database]]
- ## 角色类型
	- **登录角色** (Login Role)
		- 可以连接到数据库
		- 使用 `CREATE ROLE name LOGIN` 创建
	- **组角色** (Group Role)
		- 用于权限管理
		- 不能直接登录
- ## 常用命令
	- ```sql
		CREATE ROLE readonly;
		GRANT SELECT ON ALL TABLES TO readonly;
		```
```

## File Naming Conventions

### Namespace Mapping
- File: `pages/父页面%2F子页面.md` → Link: `[[父页面/子页面]]`
- Use `%2F` (dot) in file names
- Use `/` (slash) in Logseq links

### Examples
- File: `CommonJS%2FModule.md` → Link: `[[CommonJS/Module]]`
- File: `CSS%2F选择器.md` → Link: `[[CSS/选择器]]`

### Special Characters
- Use URL encoding for special characters if needed
- Keep page names descriptive but concise

## File Renaming Policy

**NEVER rename files without user confirmation.**

If you find a page with unexpected naming (e.g., `Postgresql.md` instead of `PostgreSQL.md`):
- Use the existing file name as-is
- Do NOT rename it automatically
- File renaming always requires explicit user approval

## Quality Checks

Before finalizing:
- [ ] Target page created or updated correctly
- [ ] Namespace mapping correct (. in filename, / in links)
- [ ] Parent page updated (if creating namespace child)
- [ ] Outline structure uses `-` and TAB indentation
- [ ] All concepts have `[[]]` links
- [ ] Chinese content properly formatted
- [ ] Block properties don't start with `-`
- [ ] NO journal entry created (this workflow skips journals)

## Common Mistakes to Avoid

1. **Don't create journal entries** - This workflow is journal-free
2. **Don't use spaces for indentation** - Always use TAB
3. **Don't forget `-` prefix** - Every block needs it (except properties)
4. **Don't assume exact file names** - Use semantic search and confirmation
5. **Don't rename files** - Always ask user first
6. **Don't forget parent page** - Update parent when creating namespace child

## Examples

### Example 1: Add namespace child page

```
User: "给 PostgreSQL 词条增加 [[PostgreSQL/role]] 相关的概念"

Actions:
1. Check if pages/Postgresql%2Frole.md exists → doesn't exist
2. Create pages/Postgresql%2Frole.md with role-related content
3. Update pages/Postgresql.md to reference [[PostgreSQL/role]]
4. No journal entry needed
```

### Example 2: Update existing page

```
User: "更新 [[React]] 页面,添加 Hooks 的说明"

Actions:
1. Find pages/React.md (or similar)
2. Read existing content
3. Add Hooks section maintaining existing structure
4. Add [[React/Hooks]] link if appropriate
5. No journal entry needed
```

### Example 3: Create new concept page

```
User: "创建一个 [[GraphQL]] 的页面"

Actions:
1. Check if pages/GraphQL.md exists → doesn't exist
2. Create pages/GraphQL.md with:
   - Appropriate tags
   - Basic structure
   - Links to related concepts
3. No journal entry needed
```

## See Also

- [Logseq Syntax Reference](references/LOGSEQ_SYNTAX.md) - Detailed syntax guide
- Use `logseq-journal-entry` skill for journal-first workflow with scattered notes
- Use `logseq-format-validator` skill to validate format before writing
