---
name: competitor-analysis
description: "Competitive content analysis across social platforms. Analyzes competitor posts, engagement patterns, content themes, posting cadence, and format diversity. Use when user says competitor analysis, competitive research, analyze competitors, competitive content audit, or what are competitors doing."
user-invokable: false
---

# Competitor Analysis

## Process

1. **Identify competitors**: user specifies 3-5 target competitors OR system identifies based on industry
2. **Collect data**: gather posts from LinkedIn, Twitter/X, Instagram (last 30 days minimum)
3. **Read references**: load `content-creation-pipeline/001-RESEARCH/skills/competitor-analysis/references/platform-content-patterns.md`
4. **Analyze per platform**: evaluate content themes, format mix, engagement rates, posting frequency
5. **Identify gaps**: find content angles competitors are missing
6. **Generate insights**: produce actionable differentiation opportunities

## What to Analyze

### Content Themes
- What topics/themes dominate their content?
- What's their unique positioning or voice?
- What pain points or benefits do they emphasize?
- What content pillars do they follow?

### Format Diversity
- Static images vs video vs carousel vs text posts
- Long-form vs short-form content
- Original content vs reshares vs engagement bait

### Engagement Patterns
- Average likes/comments/shares per post
- Which content types get highest engagement?
- Posting times and frequency
- Community response quality

### Posting Cadence
- Posts per week per platform
- Consistency patterns
- Content calendar themes (if discernible)

### Differentiation Opportunities
- Content angles NOT covered by competitors
- Format gaps (underutilized content types)
- Audience segments competitors aren't addressing
- Messaging themes competitors haven't exploited

## Quality Gates

- Minimum 30 days of posts for meaningful analysis
- Minimum 10 posts per competitor for engagement patterns
- Always compare against minimum 2 competitors
- Never recommend copying competitor content directly

## Output

### Deliverables
- `COMPETITOR-ANALYSIS.md`: Full competitive landscape analysis
- Content gap matrix
- Differentiation opportunities list
- Recommended content angles for user

### Output Format
```
Competitor Content Landscape

[Competitor A]
- Platform Mix: [platform breakdown]
- Content Themes: [top 3 themes]
- Engagement Avg: [likes/comments/shares]
- Posting Frequency: [X posts/week]
- Format Mix: [image/video/carousel %]
- Content Gaps: [what's missing]

[Competitor B]
...

Gap Analysis
[What's NOT being covered by any competitor]

Differentiation Opportunities
1. [Opportunity] - [why it works]
2. [Opportunity] - [why it works]
```
