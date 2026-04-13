---
name: logseq-file-asset-manager
description: Manage media files and assets by directly manipulating local file system. Use when user needs to add images, PDFs, documents to notes. Works by placing files in assets/ directory and generating markdown reference syntax. Does not use Plugin API.
license: MIT
---

# Logseq Asset Manager

Manage media files and assets in Logseq notes.

## When to Use This Skill

Use this skill when the user:
- Needs to add images, photos, or screenshots to notes
- Wants to attach PDF documents or other files
- References drawings or diagrams
- Asks about asset organization or file references
- Needs to update or fix asset references

## Asset Directory Structure

### Flat Structure
```
assets/
├── image_1709208804749_0.png
├── paper_2024.pdf
├── diagram_architecture.png
└── screenshot_20260414.png

draws/
├── system_architecture
└── workflow_diagram
```

**Key principles:**
- `assets/` contains ALL media files in flat structure (no subdirectories)
- `draws/` contains Logseq drawing files
- No nested folders within assets/

## Asset Types and Reference Syntax

### 1. Images (PNG, JPG, GIF, etc.)

**Syntax**: `![description](../assets/filename.ext)`

✅ Correct:
```markdown
- ![Web Architecture](../assets/architecture_diagram.png)
- ![Screenshot](../assets/screenshot_20260414.png)
```

❌ Incorrect:
```markdown
- [Image](../assets/image.png)  # Missing ! prefix
- ![Image](assets/image.png)    # Missing ../
- ![Image](/assets/image.png)   # Wrong path format
```

### 2. Documents (PDF, DOCX, etc.)

**Syntax**: `[description](../assets/filename.ext)`

✅ Correct:
```markdown
- [Research Paper](../assets/paper_2024.pdf)
- [Meeting Notes](../assets/notes_20260414.docx)
```

❌ Incorrect:
```markdown
- ![PDF](../assets/paper.pdf)   # Should not use ! for documents
- [PDF](assets/paper.pdf)       # Missing ../
```

### 3. Drawings

**Syntax**: `[[draws/filename]]`

✅ Correct:
```markdown
- 系统架构图: [[draws/system_architecture]]
- 流程图: [[draws/workflow_diagram]]
```

❌ Incorrect:
```markdown
- [Drawing](../draws/diagram)           # Wrong syntax
- [[draws/diagram.excalidraw]]          # Don't include extension
- ![Drawing](../draws/diagram.png)      # Wrong syntax
```

## Asset Naming Conventions

### Automatic Naming (Logseq default)
```
{type}_{timestamp}_{index}.{ext}

Examples:
- image_1709208804749_0.png
- file_1709208804749_0.pdf
```

### Manual Naming (recommended for clarity)
```
{descriptive_name}_{date}.{ext}

Examples:
- architecture_diagram_20260414.png
- research_paper_2024.pdf
- screenshot_login_page.png
```

**Best practices:**
- Use descriptive names when manually adding assets
- Include dates for time-sensitive content
- Use lowercase with underscores
- Avoid spaces in filenames

## Workflow

### Step 1: Determine Asset Type

Identify what type of asset the user is working with:
- **Image**: PNG, JPG, GIF, SVG, WebP → Use `![]()`
- **Document**: PDF, DOCX, XLSX, TXT → Use `[]()`
- **Drawing**: Logseq/Excalidraw drawings → Use `[[draws/]]`

### Step 2: Place File in Correct Location

**For images and documents:**
1. Place file in `assets/` directory (flat structure)
2. Use descriptive filename
3. No subdirectories

**For drawings:**
1. Place file in `draws/` directory
2. Reference by name without extension

### Step 3: Generate Reference Syntax

Based on asset type, generate the correct markdown reference:

```markdown
# Images
- ![Description](../assets/filename.png)

# Documents
- [Description](../assets/filename.pdf)

# Drawings
- [[draws/filename]]
```

### Step 4: Integrate into Outline

Add the reference within proper Logseq outline structure:

```markdown
- ## 系统架构
	- 整体架构如下图所示:
	- ![System Architecture](../assets/architecture_20260414.png)
	- 详细设计文档: [Design Doc](../assets/design_doc.pdf)
	- 交互流程图: [[draws/interaction_flow]]
```

## Common Use Cases

### Use Case 1: Adding a Screenshot

```markdown
User: "添加一个登录页面的截图"

Actions:
1. Receive or locate screenshot file
2. Place in assets/ as screenshot_login_page_20260414.png
3. Generate reference: ![Login Page](../assets/screenshot_login_page_20260414.png)
4. Add to appropriate page with outline structure
```

### Use Case 2: Attaching a PDF

```markdown
User: "把这个研究论文添加到笔记里"

Actions:
1. Receive or locate PDF file
2. Place in assets/ as research_paper_2024.pdf
3. Generate reference: [Research Paper](../assets/research_paper_2024.pdf)
4. Add to appropriate page with context
```

### Use Case 3: Referencing a Drawing

```markdown
User: "引用系统架构图"

Actions:
1. Verify drawing exists in draws/
2. Generate reference: [[draws/system_architecture]]
3. Add to appropriate page with context
```

## Fixing Asset References

### Common Issues

**Issue 1: Wrong path format**
```markdown
❌ ![Image](assets/image.png)
✅ ![Image](../assets/image.png)
```

**Issue 2: Wrong syntax for asset type**
```markdown
❌ [Image](../assets/image.png)      # Document syntax for image
✅ ![Image](../assets/image.png)     # Correct image syntax
```

**Issue 3: Drawing with wrong syntax**
```markdown
❌ ![Drawing](../draws/diagram.png)
✅ [[draws/diagram]]
```

**Issue 4: Nested directories**
```markdown
❌ ![Image](../assets/screenshots/image.png)
✅ ![Image](../assets/screenshot_image.png)
```

## Asset Organization Tips

### Keep Assets Organized
1. Use descriptive filenames
2. Include dates for time-sensitive content
3. Clean up unused assets periodically
4. Maintain flat structure in assets/

### Naming Patterns
```
# Screenshots
screenshot_{feature}_{date}.png
screenshot_login_page_20260414.png

# Diagrams
diagram_{type}_{date}.png
diagram_architecture_20260414.png

# Documents
{type}_{topic}_{date}.{ext}
paper_research_2024.pdf
notes_meeting_20260414.docx
```

## Integration with Outline Structure

Always integrate assets within proper Logseq outline:

```markdown
- ## 项目文档
	- ### 架构设计
		- 系统整体架构:
		- ![Architecture](../assets/architecture_diagram.png)
		- 详细说明参考: [Design Doc](../assets/design_doc_v2.pdf)
	- ### 流程图
		- 用户注册流程:
		- [[draws/user_registration_flow]]
		- 支付流程:
		- [[draws/payment_flow]]
```

## Quality Checks

Before finalizing:
- [ ] File placed in correct directory (assets/ or draws/)
- [ ] Filename is descriptive and follows conventions
- [ ] Reference syntax matches asset type
- [ ] Path uses `../assets/` format (not `assets/` or `/assets/`)
- [ ] Integrated within proper outline structure (starts with `-`)
- [ ] Description is meaningful and in Chinese (if applicable)
- [ ] No nested subdirectories in assets/

## Common Mistakes to Avoid

1. **Don't create subdirectories** - Keep assets/ flat
2. **Don't use wrong syntax** - Match syntax to asset type
3. **Don't forget `../` prefix** - Always use relative path with `../`
4. **Don't include extension for drawings** - Use `[[draws/name]]` not `[[draws/name.excalidraw]]`
5. **Don't forget outline structure** - Asset references need `-` prefix

## Quick Reference

| Asset Type | Location | Syntax | Example |
|------------|----------|--------|---------|
| Image | `assets/` | `![desc](../assets/file.png)` | `![Diagram](../assets/arch.png)` |
| PDF | `assets/` | `[desc](../assets/file.pdf)` | `[Paper](../assets/research.pdf)` |
| Document | `assets/` | `[desc](../assets/file.ext)` | `[Notes](../assets/notes.docx)` |
| Drawing | `draws/` | `[[draws/name]]` | `[[draws/architecture]]` |

## See Also

- Use `logseq-journal-entry` or `logseq-page-maintenance` for adding assets to notes
- Use `logseq-format-validator` to validate the complete note structure
