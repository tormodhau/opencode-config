---
name: helm-render
description: Render Helm templates for all environments to establish a diff baseline
agent: helm-render
subtask: true
---

Run helm template for all environments and save output to rendered/.
Report which files were created and flag any helm template errors.
