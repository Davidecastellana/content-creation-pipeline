---
description: FAAW Pipeline Executor - Runs content creation pipeline via MiniMax Token Plan
on:
  workflow_dispatch:
  schedule:
    - cron: "0 9 * * *"
  push:
    branches:
      - main

permissions:
  contents: read

strict: false

network:
  allowed:
    - defaults
    - api.minimax.io

engine:
  id: claude
  api-target: api.minimax.io
  max-turns: 50

tools:
  github: all
  timeout: 120

timeout-minutes: 30

env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"

safe-outputs:
  create-issue:
    title-prefix: "[pipeline] "
    labels: [automated, pipeline]
    max: 5
    close-older-issues: true
  add-comment:
    max: 10
---

# FAAW Pipeline Executor

This workflow reads your FAAW folder structure and executes the content creation pipeline stages.

## Pipeline Structure
- `CLAUDE.md` at root defines the pipeline stages
- `content-creation-pipeline/001-RESEARCH/` - Research stage
- `content-creation-pipeline/002-INTAKE/` - Intake/planning stage
- `content-creation-pipeline/003-CREATE/` - Content creation stage
- `content-creation-pipeline/004-OUTPUT/` - Output stage

## Task 1: Read Root CLAUDE.md
Read the CLAUDE.md file at the repository root to understand the pipeline structure, content types supported, and overall workflow orchestration.

## Task 2: Execute Stage 001 (Research)
1. Read `content-creation-pipeline/001-RESEARCH/CLAUDE.md`
2. Read any skill files in `content-creation-pipeline/001-RESEARCH/`
3. Execute research tasks defined in the stage
4. Output findings as artifacts or comments

## Task 3: Execute Stage 002 (Intake/Planning)
1. Read `content-creation-pipeline/002-INTAKE/CLAUDE.md`
2. Read any skill files in `content-creation-pipeline/002-INTAKE/`
3. Execute planning tasks defined in the stage
4. Output plans as artifacts or comments

## Task 4: Execute Stage 003 (Creation)
1. Read `content-creation-pipeline/003-CREATE/CLAUDE.md`
2. Read any skill files in `content-creation-pipeline/003-CREATE/`
3. Execute content creation tasks
4. Generate draft content based on research and plans

## Task 5: Execute Stage 004 (Output)
1. Read `content-creation-pipeline/004-OUTPUT/CLAUDE.md`
2. Read any skill files in `content-creation-pipeline/004-OUTPUT/`
3. Finalize and format content
4. Prepare output summary

## Output
After all stages complete, create a GitHub issue with:
- Summary of what was accomplished
- Content generated
- Any artifacts created
- Next steps recommended
