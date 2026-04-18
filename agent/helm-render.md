---
name: helm-render
description: >
  Renders Helm templates for all environments and saves to rendered/.
  Use before any refactoring session begins to establish a baseline.
mode: subagent
hidden: true
model: qwen/qwen3-coder-next-fp8
temperature: 0.0
maxSteps: 5
permission:
  edit:
    "*": deny
    "rendered/*": allow
  bash:
    "*": deny
    "helm template *": allow
    "mkdir *": allow
---

## Instructions

1. Run `mkdir -p rendered` if the directory does not exist.
2. For each `values.[env].yaml` file found in the current directory:
   - Run: `helm template . -f values.yaml -f values.[env].yaml > rendered/[env].yaml`
3. Report which files were created and whether `helm template` returned any errors.
4. Do not modify any other files.
