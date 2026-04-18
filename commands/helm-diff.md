---
name: helm-diff
description: Create diff.[env].yaml for each environment
license: MIT
compatibility: opencode
  workflow: helm
---

## What I do

- Look for rendered manifests `rendered/[env].yaml`
- If no files are found, inform the user and stop execution

- For each file found, create a `diff.[env].yaml`-file into the `/rendered`-directory with the following command:

    helm template . -f values.yaml -f values.[env].yaml | difft /rendered/[env].yaml > /rendered/diff.[env].yaml

If the `difft` tool is unavailable use `diff` instead
