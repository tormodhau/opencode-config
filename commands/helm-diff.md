---
name: helm-diff
description: Compare current Helm output against the rendered baseline
agent: helm-diff
subtask: true
---

Compare current helm template output against rendered/ baseline.
Classify changes as cosmetic or semantic.
Show a summary table and flag any semantic differences.
