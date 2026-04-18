---
name: helm-render
description: Create rendered.[env].yaml for each environment
license: MIT
compatibility: opencode
  workflow: helm
---

## What I do

- Create a `/rendered` folder if it does not already exist in the current directory:

    mkdir rendered

- Create a `[env].yaml`-file into the `/rendered`-directory for each `values.[env].yaml` file in the directory with the following commands:

    helm template . -f values.yaml -f values.dev.yaml > rendered/dev.yaml
    helm template . -f values.yaml -f values.test.yaml > rendered/test.yaml
    helm template . -f values.yaml -f values.prod.yaml > rendered/prod.yaml
