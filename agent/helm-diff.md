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

1. Find all `rendered/[env]/[working-directory].yaml` files.
2. If none found, stop and report.
3. For each [env], run:
   - `helm template [working-directory] -f values.yaml -f values.[env].yaml | difft rendered/[env]/[working-directory].yaml -`
   - If `difft` is unavailable: `helm template . -f values.yaml -f values.[env].yaml | difft rendered/[env]/[working-directory].yaml -`
4. Save each diff to `rendered/[env].diff-[working-directory].txt`.
5. Classify each diff: cosmetic only (whitespace, comments, ordering) vs semantic (value changes, added/removed resources, spec changes).
6. Return a summary table:

| Env | Diff file | Semantic changes? | Details |
|-----|-----------|-------------------|---------|

If semantic changes are found, show the relevant diff lines.
