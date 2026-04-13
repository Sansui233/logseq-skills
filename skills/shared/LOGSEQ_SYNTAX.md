# Logseq Outlined Markdown Syntax Reference

Complete reference for Logseq's extended markdown syntax.

## Core Principles

1. **Block-based outline**: Everything is a block starting with `-`
2. **TAB indentation**: Use TAB (not spaces) for hierarchy
3. **Extended markdown**: Headings, lists, and code blocks all need `-` prefix

## Outline Structure

### Basic Blocks

```markdown
- Block content
	- Nested block (TAB indented)
		- Deeper nested block (TAB indented)
```

### Indentation Rules

- **MUST use TAB** for indentation
- **NEVER use spaces** for indentation
- Each level = one TAB character
- Consistent hierarchy (no skipped levels)

## Extended Markdown Elements

### Headings

All headings must start with `-`:

```markdown
- # Heading 1
- ## Heading 2
- ### Heading 3
- #### Heading 4
```

### Ordered Lists

Ordered lists must start with `-`:

```markdown
- 1. First item
- 2. Second item
- 3. Third item
```

### Unordered Lists

Standard blocks are unordered list items:

```markdown
- Item one
- Item two
	- Nested item
```

### Code Blocks

Code blocks must start with `-`:

```markdown
- ```javascript
	const x = 1;
	console.log(x);
	```
```

```markdown
- ```python
	def hello():
		print("world")
	```
```

## Text Formatting

### Inline Formatting

```markdown
- **Bold text**
- *Italic text*
- ^^Highlight^^ or ==Highlight==
- ~~~Strikethrough~~~
- `inline code`
- <ins>Underline</ins>
```

### Combined Formatting

```markdown
- **Bold with `code` inside**
- *Italic with [[link]]*
```

## Links and References

### Page Links

```markdown
- [[Page Name]]
- [[Parent/Child]] (namespace)
- [Display Text]([[Page Name]])
```

### Block References

```markdown
- ((block-uuid))
- Reference to specific block
```

### External Links

```markdown
- [Link Text](https://example.com)
- https://example.com (auto-linked)
```

## Properties

### Page Properties

At the top of file, **no `-` prefix**:

```markdown
tags:: tag1, tag2
author:: John Doe
type:: article
```

### Block Properties

After block content, **no `-` prefix**:

```markdown
- **Block title**
	collapse:: true
	- Block content
```

Common block properties:
- `collapse:: true` - Make block collapsible
- `id:: custom-id` - Custom block ID

## Namespace Convention

### File to Link Mapping

- File name uses `.` (dot) separator
- Logseq links use `/` (slash) separator

| File Name | Link Syntax |
|-----------|-------------|
| `Parent.Child.md` | `[[Parent/Child]]` |
| `JavaScript.Array.md` | `[[JavaScript/Array]]` |
| `CSS.选择器.md` | `[[CSS/选择器]]` |

### Examples

```markdown
File: pages/PostgreSQL.role.md
Link: [[PostgreSQL/role]]

File: pages/CommonJS.Module.md
Link: [[CommonJS/Module]]
```

## Special Features

### Tasks

```markdown
- TODO Task to do
- DOING Task in progress
- DONE Completed task
- LATER Task for later
- NOW Current task
```

### Scheduled and Deadlines

```markdown
- TODO Review PR
	SCHEDULED: <2026-04-14 Mon>
	DEADLINE: <2026-04-15 Tue>
```

### Tags

```markdown
- Inline tag: #tag-name
- Multiple tags: #frontend #javascript
```

### Queries

```markdown
- {{query (and [[tag1]] [[tag2]])}}
```

## Asset References

### Images

```markdown
- ![Description](../assets/image.png)
- ![Architecture Diagram](../assets/arch_diagram.png)
```

### Documents

```markdown
- [PDF Document](../assets/document.pdf)
- [Research Paper](../assets/paper_2024.pdf)
```

### Drawings

```markdown
- [[draws/diagram_name]]
- [[draws/architecture]]
```

## Complete Example

```markdown
tags:: 数据库, PostgreSQL
author:: Developer

- ## PostgreSQL 概述
	- [[PostgreSQL]] 是一个强大的开源关系数据库
	- 相关概念: [[PostgreSQL/role]], [[PostgreSQL/schema]]
- ## 架构
	collapse:: true
	- 三层结构:
		- 1. Database
		- 2. Schema
		- 3. Table
	- 对比 [[MySQL]] 只有两层
- ## 代码示例
	- ```sql
		CREATE DATABASE mydb;
		CREATE SCHEMA myschema;
		CREATE TABLE myschema.users (id INT);
		```
- ## 参考资料
	- [Official Docs](https://postgresql.org/docs)
	- ![Architecture](../assets/pg_architecture.png)
	- [[draws/pg_architecture_diagram]]
```

## Common Mistakes

### ❌ Missing dash prefix

```markdown
Content without dash
## Heading without dash
```

### ❌ Space indentation

```markdown
- Parent
  - Child (spaces)
```

### ❌ Property with dash

```markdown
- tags:: value
- collapse:: true
```

### ❌ Wrong namespace separator

```markdown
File: Parent/Child.md
Link: [[Parent.Child]]
```

### ❌ Code block without dash

````markdown
```javascript
code
```
````

## Correct Versions

### ✅ Dash prefix

```markdown
- Content with dash
- ## Heading with dash
```

### ✅ TAB indentation

```markdown
- Parent
	- Child (TAB)
```

### ✅ Property without dash

```markdown
tags:: value
collapse:: true
```

### ✅ Correct namespace separator

```markdown
File: Parent.Child.md
Link: [[Parent/Child]]
```

### ✅ Code block with dash

```markdown
- ```javascript
	code
	```
```

## Quick Reference Table

| Element | Syntax | Example |
|---------|--------|---------|
| Block | `- content` | `- 这是一个块` |
| Nested | `- parent`<br>`	- child` | TAB indent |
| Heading | `- ## heading` | `- ## 标题` |
| Ordered | `- 1. item` | `- 1. 第一项` |
| Code | `- ```lang`<br>`	code`<br>`	```` | See above |
| Page link | `[[page]]` | `[[PostgreSQL]]` |
| Namespace | `[[parent/child]]` | `[[PostgreSQL/role]]` |
| Block ref | `((uuid))` | `((abc-123))` |
| Property | `key:: value` | `tags:: 数据库` |
| Image | `![desc](../assets/file)` | `![Diagram](../assets/d.png)` |
| Document | `[desc](../assets/file)` | `[PDF](../assets/doc.pdf)` |
| Drawing | `[[draws/name]]` | `[[draws/architecture]]` |
