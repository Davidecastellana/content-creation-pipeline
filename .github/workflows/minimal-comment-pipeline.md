---
description: |
  Minimal 2-stage pipeline with human-in-loop via GitHub issue comments.
  Stage 0: Initialize and wait. Stage 1: Read brief and complete.
  User must manually trigger each stage.
on:
  workflow_dispatch:
    inputs:
      stage:
        description: "Stage to execute (0 or 1)"
        required: false
        default: "0"

permissions:
  contents: read
  issues: read
  pull-requests: read

safe-outputs:
  create-issue:
    labels: [automated, pipeline]
  add-comment:
    max: 5

strict: false

network:
  allowed:
    - defaults
    - api.minimax.io

engine:
  id: claude
  api-target: api.minimax.io
  max-turns: 20

tools:
  github: all
  timeout: 180

timeout-minutes: 30

env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
---

# Minimal 2-Stage Pipeline

You are executing a 2-stage FAAW pipeline. The input `stage` determines which stage to run.

## Stage 0: Initialize (when stage input is "0" or empty)

1. Create directory `content-creation-pipeline/000-INIT/outputs/`
2. Create `content-creation-pipeline/000-INIT/outputs/STATUS.md` with:
   ```
   Pipeline Stage: 0
   Status: COMPLETE
   Timestamp: [current datetime]
   Waiting for: User comment on Issue #6 with brief content
   
   To continue: Manually trigger workflow_dispatch with stage=1, then add brief as comment on Issue #6
   ```
3. Add a comment to Issue #6: "Stage 0 complete. Pipeline waiting for brief on Issue #6. Trigger stage=1 after commenting."

## Stage 1: Process Brief (when stage input is "1")

1. Read ALL comments on Issue #6 to find the user's brief content
2. Parse the brief from the most recent relevant comment
3. Create directory `content-creation-pipeline/001-PROCESS/outputs/`
4. Create `content-creation-pipeline/001-PROCESS/outputs/RESULT.md` with:
   - Brief summary: [extracted from comment]
   - Stage: 1
   - Status: COMPLETE
   - Timestamp: [current datetime]
5. Add a comment to Issue #6 confirming: "Stage 1 complete. Brief received and processed. Pipeline finished."