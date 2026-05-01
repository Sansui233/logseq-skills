---
name: logseq-to-obsidian
description: Convert Logseq formatted markdown to Obsidian format
---

## When to use

when user ask you to convert logseq markdown file into obsidian.

## Convert Rule

### Metadata

At the first block of the page, > convert to standard markdown yaml frontmatter:

From

```logseq
- alias:: xxx
    tags:: xxx, xxx
    icon:: xxx
```

To

```md
---
alias: xxx
tags:
  - xxx
  - xxx
icon: xxx
```

### Remove logseq block property

From
```logseq
- text text text text
    collapse:: true
```

To
```markdowm
- text
```

### Fix Internal Link

Link internal page with external Link grammar is different in Obsidian.

From

```logseq
[综述]([[📄Sentiment Analysis and Opinion Mining]])
```

To

```md
[[📄Sentiment Analysis and Opinion Mining|综述]]
```

### Remove/fix Outline

1. Heading should not be outlined.

From `- ## Heading` to `## Heading`(No indentation)

2. Quote can't be outlined in Obsidan

From `- > xxx说：xxx` To `> xxx 说xxx` (No indentation)

3. If some height-Level list should be heading symatically, make it Heading. It depends on context

### Namespace Convert

In logseq, all file is flattened in pages dir, And followed it's special namespace grammar. But in Obsidian, namspace is just a folder. You should
- Create corresponding namespace folder
- Put all [[namespace.xxx.md]] file in to namespace folder
- For files in namespace folder, remove the namespace prefix

### File name checking

In obsidian, `#` is regared as heading anchor, `|` is alias, `^` is block ref mark. Avoid markdown file name and directory name with `# | ^ : %% [[ ]]` and follow the safe file name rule on both windows and linux.

Marks forbidden on Windows OS:
< (less than)
> (greater than)
: (colon - sometimes works, but is actually NTFS Alternate Data Streams)
" (double quote)
/ (forward slash)
\ (backslash)
| (vertical bar or pipe)
? (question mark)
* (asterisk)

forbidden on Linux/Unix:
- / (forward slash)


## Quality Checks

- internal Link repaired
- block property removed
- frontmatter rewrite
- outline removed/fixed
- namespace convert
- safe file name
