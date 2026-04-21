---
name: helm-diff
description: >
  Compares current helm template output against the baseline in rendered/.
  Reports whether any non-cosmetic (semantic) differences were found.
mode: subagent
hidden: true
model: nhn-provider/nhn-coder
temperature: 0.0
maxSteps: 5
permission:
  edit:
    "*": deny
    "rendered/*": allow
  bash:
    "*": deny
    "helm template *": allow
    "difft *": allow
    "diff *": allow
---

## Instructions

1. Run /helm-render
2. Use git to diff what has changed from the previous commit
3. Classify each diff:
    a) cosmetic only (whitespace, comments, ordering) vs
    b) semantic (value changes, added/removed resources, spec changes).
4. Return a summary table:

| Env | File Name Diffed | Semantic changes? | Details |
|-----|-----------|-------------------|---------|

If semantic changes are found, show the relevant diff lines.
