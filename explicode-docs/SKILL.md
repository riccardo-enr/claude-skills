---
name: explicode-docs
description: Add or update Explicode-compatible documentation in code files. Explicode renders Markdown from code comments (block comments for C/C++/CUDA, triple-quote docstrings for Python). Use when the user asks to document files with Explicode.
disable-model-invocation: true
allowed-tools: Read, Edit, Glob, Grep
---

Add or update documentation in the specified files using Explicode-compatible format.

## Explicode Format Rules

Explicode is a VS Code extension that renders Markdown from code comments side-by-side with the code. The documentation lives in comments and has no effect on the build.

### C / C++ / CUDA (`.c`, `.cpp`, `.cu`, `.cuh`, `.h`, `.hpp`)

Use `/* ... */` block comments with Markdown inside:

```cpp
/*
# Module Title

Description with **bold**, `inline code`, and lists.

## Section

- Item one
- Item two

$$E = mc^2$$
*/
```

- Single-line `//` comments are NOT rendered by Explicode — always use `/* ... */`.
- JSDoc-style `/** ... */` also works (leading `*` are stripped automatically).

### Python (`.py`)

Use triple-quoted strings (`"""` or `'''`) at the **start of a line** (module, class, or function level):

```python
"""
# Module Title

Description with **bold**, `inline code`, and lists.

## Section

- Item one
- Item two
"""
```

- Triple-quotes used as string values mid-expression are NOT rendered.
- Place the opening `"""` on its own line for best rendering.

### General Markdown Guidelines

- Use `#` headings to structure the documentation.
- Use fenced code blocks (` ```bash `, ` ```cpp `, etc.) for usage examples.
- Use `**bold**` for emphasis, `` `backticks` `` for code references.
- Use bullet lists (`-`) or numbered lists (`1.`) for enumerations.
- LaTeX math is supported: inline `$...$` and display `$$...$$`.
- Keep documentation concise and focused on what the file/module does.

## Steps

1. Read the target file(s) to understand their purpose and structure.
2. Check if there is existing documentation (block comments or docstrings at the top of the file).
3. Write or update the documentation using the correct Explicode format for the language:
   - For C/C++/CUDA: a `/* ... */` block comment before the first `#include`.
   - For Python: a `"""..."""` module-level docstring before imports.
4. Include at minimum:
   - A `#` title describing the file/module.
   - A brief description of what it does.
   - Key interfaces (subscriptions, publications, parameters, functions) where relevant.
5. Do not add inline `//` or `#` comments throughout the code — only top-level doc blocks.
6. Do not modify any code logic, only documentation comments.

$ARGUMENTS
