---
description: |
  Minimal 2-stage pipeline with human-in-loop via GitHub issue comments.
  Stage 0 executes on workflow_dispatch, then user comments on issue.
  Stage 1 executes on next workflow_dispatch, reading the comment as input.

on:
  workflow_dispatch:
    inputs:
      stage:
        description: "Stage to execute (0 or 1)"
        required: false
        default: "0"

permissions:
  contents: read
  issues: write

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
  filesystem: all
  prompt: all

env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"

stages:
  stage_0_initialize:
    condition: "stage == '0' || stage == ''"
    mode: AUTO
    description: "Initialize pipeline - gather context, wait for brief"
    prompt: |
      You are executing Stage 0 of a 2-stage pipeline.

      Your task:
      1. Create directory `content-creation-pipeline/000-INIT/outputs/`
      2. Create `content-creation-pipeline/000-INIT/outputs/STATUS.md` with:
         ```
         Pipeline Stage: 0
         Status: COMPLETE
         Waiting for: User comment on Issue #6
         
         To continue: Trigger workflow_dispatch with stage=1
         ```
      
      3. Comment on Issue #6:
         "Stage 0 complete. Please add your brief as a comment to continue to Stage 1."
      
      4. Output: `{"stage": "0", "status": "complete", "next_action": "dispatch_stage_1"}`

  stage_1_process:
    condition: "stage == '1'"
    mode: HYBRID
    description: "Read user's brief and complete pipeline"
    prompt: |
      You are executing Stage 1 of the pipeline.

      Your task:
      1. Read the latest comment on Issue #6 to get the brief content
      
      2. Create `content-creation-pipeline/001-PROCESS/outputs/RESULT.md` with:
         - Brief summary extracted from the comment
         - Stage: 1
         - Status: COMPLETE
         - "Pipeline finished successfully"
      
      3. Comment on Issue #6 confirming completion
      
      4. Exit with output: `{"stage": "1", "status": "success", "complete": true}`