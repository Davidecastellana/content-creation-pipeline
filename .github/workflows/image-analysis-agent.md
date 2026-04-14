---
description: Image Analysis Agent - Analyzes images using MiniMax with vision
on:
  workflow_dispatch:
    inputs:
      image-url:
        description: "URL or path to image"
        required: false
        default: "https://picsum.photos/200"

permissions:
  contents: read

strict: false

network:
  allowed:
    - defaults
    - api.minimax.io
    - picsum.photos

engine:
  id: claude
  api-target: api.minimax.io
  max-turns: 10

tools:
  github: all
  web-fetch:
  timeout: 120

timeout-minutes: 10

env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"

safe-outputs:
  add-comment:
    max: 5
---

# Image Analysis Agent

Analyze the provided image URL and create markdown documentation.

## Task

1. **Fetch Image**: Download image from `${{ inputs.image-url }}`
2. **Analyze**: Use MiniMax-M2.7 vision to describe the image
3. **Document**: Create detailed analysis in `outputs/image-analysis.md`

## Output Format

Create markdown file with:
- Image summary (1 paragraph)
- Visual elements breakdown
- Content analysis
- Technical notes

## Execute

1. Download image from input URL
2. Base64 encode it
3. Send to MiniMax with analysis prompt
4. Write response to `outputs/image-analysis.md`
5. Add comment with summary

## Important

- Use web-fetch tool to retrieve image
- Convert to base64 for API call
- Create readable analysis output