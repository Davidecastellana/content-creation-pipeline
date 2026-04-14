# GitHub Agentic Workflows + MiniMax Token Plan Configuration

## The Winning Configuration

```yaml
---
description: Your workflow description here
on:
  workflow_dispatch:

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
---

# Workflow Title

Your workflow instructions here.
```

## Why This Works

| Component | Purpose |
|-----------|---------|
| `api-target: api.minimax.io` | Routes AWF API proxy to MiniMax instead of Anthropic |
| `ANTHROPIC_API_BASE_PATH: "/anthropic"` | Adds the required path prefix for MiniMax endpoint |
| `network.allowed` | Whitelists api.minimax.io for network access |
| `ANTHROPIC_BASE_URL` | Fallback URL for Claude Code direct calls |
| `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"` | Prevents Claude Code from calling Anthropic directly |

## Key Settings Explained

### Engine Configuration

```yaml
engine:
  id: claude                    # Use Claude Code engine
  api-target: api.minimax.io   # Custom API proxy target (CRITICAL)
  max-turns: 50                # Max conversation turns
  # version: beta              # Optional: specific engine version
  # model: MiniMax-M2.7        # Optional: specific model (can also use env)
```

### Network Configuration

```yaml
network:
  allowed:
    - defaults                 # Includes standard development domains
    - api.minimax.io          # REQUIRED: Whitelist MiniMax API
    # Add other domains as needed:
    # - api.openai.com
    # - your-custom-provider.com
```

### Environment Variables (CRITICAL)

```yaml
env:
  # Required for MiniMax Token Plan
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  
  # Required: Prevents Claude Code from calling Anthropic directly
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
```

### Permissions

```yaml
permissions:
  contents: read              # Required for GitHub tools
  issues: read               # If using issues tools
  pull-requests: read        # If using PR tools
  # Add write permissions only via safe-outputs, not here
```

### Safe Outputs (Preferred for Write Operations)

```yaml
safe-outputs:
  create-issue:
    title-prefix: "[ai] "
    labels: [automation]
    max: 5
  add-comment:
    max: 3
```

## Common Pitfalls

### ❌ Wrong: Missing api-target

```yaml
# This fails - API proxy routes to wrong endpoint
engine:
  id: claude
  max-turns: 50
```

### ❌ Wrong: Missing network allowlist

```yaml
# This fails - api.minimax.io is blocked
network:
  allowed:
    - defaults
    # Missing api.minimax.io!
```

### ❌ Wrong: Missing CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC

```yaml
# This may cause Claude Code to call Anthropic directly
env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  # Missing the disable flag!
```

### ✅ Correct: Full Working Config

```yaml
---
on:
  workflow_dispatch:

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
---

# Your workflow here
```

## Alternative Providers

### For Standard Anthropic API (no proxy redirect needed)

```yaml
env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  # No ANTHROPIC_BASE_URL needed - defaults to api.anthropic.com
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
  # No api-target needed - uses default
```

### For OpenAI-Compatible Providers

```yaml
network:
  allowed:
    - defaults
    - api.openai.com

engine:
  id: claude
  # Use OpenAI-compatible endpoint in ANTHROPIC_BASE_URL
  # Note: Claude Code uses Anthropic API format, so OpenAI must be compatible
```

### For Z.ai (GLM models)

```yaml
network:
  allowed:
    - defaults
    - api.z.ai

env:
  ANTHROPIC_API_KEY: "${{ secrets.ZAI_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.z.ai/api/anthropic"
  ANTHROPIC_API_TARGET: "api.z.ai"
  ANTHROPIC_API_BASE_PATH: "/api/anthropic"
  ANTHROPIC_MODEL: "GLM-5"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
```

## Minimal Working Example

```yaml
---
on: workflow_dispatch
permissions: contents: read
strict: false
network:
  allowed:
    - defaults
    - api.minimax.io
engine:
  id: claude
  api-target: api.minimax.io
env:
  ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}"
  ANTHROPIC_BASE_URL: "https://api.minimax.io/anthropic"
  ANTHROPIC_API_TARGET: "api.minimax.io"
  ANTHROPIC_API_BASE_PATH: "/anthropic"
  ANTHROPIC_MODEL: "MiniMax-M2.7"
  CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC: "1"
---

Say hello world.
```

## GitHub Secrets Required

Set these in your repository settings → Secrets and variables → Actions:

| Secret Name | Value |
|-------------|-------|
| `ANTHROPIC_API_KEY` | Your MiniMax Token Plan API key (starts with `sk-cp-`) |

## Compilation & Deployment

```bash
# Compile workflow
gh aw compile

# Commit compiled .lock.yml
git add .github/workflows/*.lock.yml
git commit -m "Add workflow"
git push

# Run manually
gh aw run workflow-name --repo owner/repo
```

## Security Notes

1. **API keys are in the proxy sidecar** - Not directly in the agent container (when using api-proxy)
2. **Network is firewalled** - Only whitelisted domains are accessible
3. **Use safe-outputs** for write operations instead of direct GitHub API access
4. **Rotate exposed keys** - If keys are ever exposed in logs or chat, rotate immediately at the provider
