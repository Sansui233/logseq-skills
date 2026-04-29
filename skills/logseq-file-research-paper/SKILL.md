---
name: logseq-file-research-paper
description: research and make notes for academic paper or scientific deep research.
license: MIT
---

# Logseq Reasearch

Maintain knowledge graph and create/update notes for specific filed or paper.

## When to Use This Skill

Use this skill when the user
- Ask you to summarize/learning a academic paper
- Ask you to research a scientific field

## Assets management

You should place assets in to `assets/` folder, And reference the assets with logseq assets grammar `![name](../assets/filename)`

## Workflow

### 1. Scenario: summarize a paper

- Find/Create a paper about this paper in `pages/`. Just use the paper name as page file name. If some symbol(like `/`) are not supported in file name, convert is with URL encoding.
- Make the paper metadata in following format on the top of paper page:
```md
---
title: 📄 Original title without url encoding
category: paper
tags: 情感分析, RNN
year: 2021
author: Socher
description: RNN 实现的句法分析树
---
```
- Read the original paper. If PDF provided, download it into asset and link it. If HTML URL provided, link the original url in notes.
- Summarize the paper in Chinese(Don't translate terms)。核心要求：参考 Logseq Grammar 相关 skill，内容必须严格依照原文情况编写，附上原文assets 或者 link。不可编造文献，没有的部分说没有提到/不知道。
  - 所属领域
  - 论文有什么贡献
  - (Optional)算法类论文：相于目前的方法，有什么改进
  - (Optional)实验，是什么评价指标，和哪些模型相比的
  - (Optional)论文中有没有提到不足之处
- If new page created. Record it to today's Journal.

### 2. Scenario: Deep Research
- Reasearch the recent advanced academic paper, use academia mcp to search authorized academic paper. use web search aas extra information.
- Download academic paper(if pdf provided) into assets
- Write research summary into relaive page. You should if corresponding page existing or not, and create/update it. Write With assets/url references in Chinese(Don't translate terms). The paper assets must note the main model/methods and year like:
```md
xxx 提出的 [SG-AGI](../assets/xxxx.pdf) (2021) 模型在 xxx 的基础上，增加了xx，以解决xxx
xxx 提出的 [SG-AGI](https://xxxx.com/xxxx) (2021) 模型在 xxx 的基础上，增加了xx，以解决xxx
```
  - If the paper is existing in knowledge graph. use link like:
```md
xxx 提出的 [SG-AGI]([[SG-AGI Page Link]]) 模型在 xxx 的基础上，增加了xx，以解决xxx
```
- Update relative wiki term. For example, if [[方面级情感分析个性化调研报告]] is created. You should record this into 
[[ABSA]] or [[方面级情感分析]]"

## Quality Checking
- Follow logseq grammar skill
- Follow assets management guideline
- All content should came from references.
- Do not make up Terms. Use existing terminology.


