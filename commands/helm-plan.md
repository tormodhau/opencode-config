---
name: helm-plan
description: >
  Analyse the current Helm chart and produce a structured PLAN.md refactoring table.
  Uses the reasoning model. No files are modified (read-only analysis).
agent: helm-plan
subtask: false
---

Read all files in the current directory:

- values.yaml
- values.*.yaml
- templates/
- _helpers.tpl (if present)
- Chart.yaml

Analyse the chart for refactoring opportunities based on these goals:

1. values.[env].yaml should contain ONLY values that differ between environments
2. values.yaml and values.[env].yaml should be as small as possible
3. _helpers.tpl functions are only justified when they remove >3 instances of duplication
4. Remove all Helm code that exists only for chart sharing

Write PLAN.md with a numbered TODO table (columns: #, Area, What to change, Risk, Effort).
Stop after writing PLAN.md. Do not implement any changes.
