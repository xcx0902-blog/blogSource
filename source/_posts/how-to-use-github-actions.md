---
title: How to use GitHub Actions
date: 2023-01-18 19:02:05
tags:
  - GitHub
  - Instruction
---

GitHub Actions is designed to run your jobs in a free runner from a repository.

The jobs are like "publish your own blog" or "build docker" and so on.

## How to use

First, you need a GitHub account. Register a GitHub account at [here](https://github.com/signup).

Next, create a repository [here](https://github.com/new). You can name the repository with any name you want.

Then, create a file in the repository that you created called `.github/workflows/<name>.[yml/yaml]`. Fill it with the following:

```yaml
name: <workflow_name>

on:
  push: # You want to run the workflow when there's a push operation in the following branches
    branches: ["main", ...]
  pull_request: # You want to run the workflow when there's a pull_request operation in the following branches
    branches: ["main", ...]
  workflow_dispatch # You want to run the workflow manually at the action page

jobs:
  build:
    runs_on: [ubuntu-latest/windows-latest/macos-latest] # Filled with the machine type you want to use
    steps:
      - uses: actions/checkout@v3 # clone the repository to runner's work directory
      - name: <step_name>
        run: <command_you_want_to_run>
      - name: <step_name>
        run: |
          <multi_commands>
      ...
  deploy:
    ...
  ...
```
If you set it automatically run after push or pull request operations, you're already done. If you set `workflow_dispatch`, go to Action page, then you can find your defined workflow `<workflow_name>` in the left sidebar. Click it, then choose `Run workflow` and click `Run workflow` to run the workflow.
