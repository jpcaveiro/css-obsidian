---
name: workspace-qa
description: 'Answer questions using only PDF and markdown files in the project folder. Use when: user asks about course content, lecture notes, concepts, definitions, exercises, or any topic that should be grounded in the project documents. Do NOT answer from general knowledge — retrieve content from .md or .pdf files in the workspace first.'
argument-hint: 'Your question about the project content'
---

# Workspace Q&A (PDF & Markdown only)

## Purpose

Answer questions **exclusively** from the content of `.md` and `.pdf` files found in the project folder. Do not use general knowledge to fill gaps — if the answer is not in the project files, say so explicitly.

## When to Use

- User asks a question about course material, lecture topics, definitions, or exercises
- User wants to know if a concept is covered in the notes
- User needs a citation or quote from a specific document

## Procedure

### 1. Understand the question
Read the user's question carefully. Identify the key terms and concepts being asked about.

### 2. Search the workspace
Use `grep_search` or `semantic_search` to find relevant content across all `.md` and `.pdf` files in the project:
- Search for key terms from the question
- Broaden the search with synonyms or related terms if the first search returns nothing
- Use `file_search` with `**/*.pdf` to locate all PDF files before reading them (PDFs are currently in `_slides_/` but may appear anywhere in the workspace)
- Look in all subfolders — do not assume a fixed location for PDFs

### 3. Read the relevant files
Once candidate files are identified, read the relevant sections. Prioritize:
- `_math_concepts_/` — definitions and formal descriptions
- `_slides_/` — lecture content
- `_llm_faq/` — question-answer pairs on covered topics
- `_cognitive_alignment_/` — methodology and reasoning guides

### 4. Compose the answer
- Answer using only what is found in the retrieved files
- Quote or paraphrase directly; do not add outside knowledge
- If multiple files are relevant, synthesize across them

### 5. Cite your sources
Always end with a "Sources" section listing the files used, e.g.:
> **Sources:** [_math_concepts_/beta distribution.md](_math_concepts_/beta distribution.md), [_slides_/C2 Monte Carlo univariate/mc_02integration.md](_slides_/C2 Monte Carlo univariate/mc_02integration.md)

### 6. If no content is found
State clearly: "I could not find information about this in the project files." Do not guess or use general knowledge.

## Quality Checks

- [ ] Answer is grounded in retrieved file content, not general knowledge
- [ ] Source files are cited
- [ ] If nothing was found, the user is told explicitly
- [ ] No hallucinated file names or fabricated quotes
