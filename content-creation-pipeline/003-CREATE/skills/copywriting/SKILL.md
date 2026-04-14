---
name: copywriting
description: "Compelling copy generation for social media content. Writes engaging headlines, body text, and CTAs optimized for each platform. Use when user says write copy, generate copy, content copy, social copy, ad copy, or create content."
user-invokable: false
---

# Copywriting

## Process

1. **Read inputs**: campaign brief, content angles, topic calendar
2. **Read references**: load `content-creation-pipeline/003-CREATE/skills/copywriting/references/copy-frameworks.md`
3. **Select framework**: AIDA, PAS, BAB, 4P, FAB, or Star-Story-Solution based on goal
4. **Generate copy variants**: create 3-5 versions per content piece
5. **Validate character counts**: enforce platform limits
6. **Apply brand voice**: match tone of voice from brief
7. **Output copy deck**: organized by platform and content type

## Copy Frameworks

### AIDA (Awareness → Action)
- **A**ttention: Hook in first 3 words
- **I**nterest: Detail and supporting points
- **D**esire: Benefit-focused emotional appeal
- **A**ction: Clear CTA

### PAS (Problem → Agitate → Solution)
- **P**roblem: State the pain point
- **A**gitate: Amplify the pain
- **S**olution: Present your solution

### BAB (Before → After → Bridge)
- **B**efore: Current pain state
- **A**fter: Desired state with your solution
- **B**ridge: How to get from before to after

### 4P (Promise → Picture → Proof → Push)
- **P**romise: Compelling headline
- **P**icture: Vivid benefit visualization
- **P**roof: Social proof or data
- **P**ush: CTA

### FAB (Feature → Advantage → Benefit)
- **F**eature: What it is
- **A**dvantage: Why it's better
- **B**enefit: What the user gets

### Star-Story-Solution (Brand Storytelling)
- **S**tar: Character introduction
- **S**tory: Narrative arc with conflict
- **S**olution: Resolution with product/service

## Platform Copy Rules

### LinkedIn
- **Single Post**: 150-300 words, hook in first line (visible without "see more")
- **Article**: 1,500-3,000 words, structured with headers
- **Document Post**: PDF-style carousel, 10-15 slides
- **Hook rules**: No questions as first line, lead with value

### Twitter/X
- **Single Tweet**: 100 chars max, clear message in first 90
- **Thread**: 3-15 tweets, each tweet standalone-readable
- **Hook**: Bold statement or contrarian take in tweet 1
- **Thread structure**: 1 (hook) + N-2 (content) + 1 (CTA)

### Instagram
- **Caption**: 150-500 chars for feed, 100 chars for Stories
- **Hook**: Line 1-2 must hook before "more" cut-off
- **CTA**: End with question or clear action
- **Hashtags**: 3-5 relevant, 1-2 branded

## Copy Quality Rules

- **Never exceed character limits**; truncated copy destroys engagement
- **Always show character count** in parentheses
- **Hook in first 3 words**; first line must stop the scroll
- **Active voice only**; no passive constructions
- **Every CTA must have action verb + benefit**
- **Numbers work**: include specific stats where relevant
- **No clickbait**: headlines must deliver on promise

## Character Limits by Platform

| Platform | Content Type | Limit |
|----------|-------------|-------|
| LinkedIn | Post text | No hard limit, 150-300 optimal |
| LinkedIn | Article | No limit, 1,500-3,000 optimal |
| Twitter/X | Single tweet | 280 chars |
| Twitter/X | Thread tweet | 280 chars |
| Instagram | Feed caption | 2,200 chars |
| Instagram | Story caption | 150 chars |

## Output

### Deliverables
- `COPY-DECK.md`: Complete copy for all content pieces
- Copy validated and character-counted
- Organized by platform and post type

### Output Format
```markdown
# Copy Deck: [Campaign/Topic]

## LinkedIn Post

**Headline:** [Hook line]
**Body:**
[Copy text - 150-300 words]

**CTA:** [Action verb + benefit]
**Hashtags:** [3-5 relevant]

**Character count:** [XXX] / [limit]

---

## Twitter Thread

**Tweet 1 (Hook):**
[Standalone hook - 100 chars max]
(XX chars)

**Tweet 2:**
[Content continuation]
(XX chars)

**Tweet 3:**
[More content]
(XX chars)

**Tweet N (CTA):**
[Engagement CTA]
(XX chars)

---

## Instagram Caption

**Hook:** [First 2 lines - visible before "more")]
**Body:**
[Main caption content]

**CTA:** [Question or action]
**Hashtags:** [3-5 relevant]

**Character count:** [XXX] / 2,200
```
