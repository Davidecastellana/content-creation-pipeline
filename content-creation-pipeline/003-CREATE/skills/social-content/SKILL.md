---
name: social-content
description: "Social media content creation for LinkedIn, Twitter/X, and Instagram. Generates platform-specific posts, threads, captions, and content calendars. Use when user says social content, social media posts, LinkedIn post, Twitter thread, Instagram caption, or content calendar."
user-invokable: false
---

# Social Content

## Process

1. **Read inputs**: copy deck, content brief, topic calendar
2. **Identify platform**: determine best platform for each content piece
3. **Read references**: load `content-creation-pipeline/003-CREATE/skills/social-content/references/platform-specs.md`
4. **Generate content variants**: create platform-optimized versions
5. **Apply platform nuances**: hashtags, emojis, formatting
6. **Validate against brief**: ensure goals and tone are met
7. **Assemble content calendar**: organize by date and platform

## Platform-Specific Rules

### LinkedIn
- **Algorithm favors**: conversations, comments, saves (not just likes)
- **Best times**: Tuesday-Thursday, 8am-10am, 5pm-6pm local
- **Hook strategy**: No questions in first line, lead with value statement
- **Hashtags**: 3-5 relevant, 1-2 niche-specific
- **Document posts**: PDF carousel with 10-15 slides performs well
- **Article format**: Long-form with headers for thought leadership

### Twitter/X
- **Algorithm favors**: early engagement (first 30 minutes), replies
- **Best times**: Tuesday-Thursday, 8am-10am, 12pm-1pm local
- **Hook strategy**: Bold statement, contrarian take, or curiosity gap in tweet 1
- **Thread structure**: 1 hook + N content + 1 CTA
- **Hashtags**: 1-2 relevant, embedded mid-thread or at end
- **Engagement**: Ask questions, run polls, cite others

### Instagram
- **Algorithm favors**: saves, shares, engagement rate (not just likes)
- **Best times**: Monday-Thursday, 11am-1pm, 7pm-9pm local
- **Hook strategy**: Line 1-2 must hook before "...more" cut-off
- **Visual first**: copy supports image/video, doesn't lead with it
- **Hashtags**: 3-5 relevant (can be in first comment)
- **Stories**: Use stickers, polls, questions for engagement

## Content Types by Platform

### LinkedIn
- **Single image post**: Text + image, 150-300 words
- **Document post**: PDF carousel, 10-15 slides
- **Article**: Long-form thought leadership, 1,500-3,000 words
- **Video posts**: Native video up to 10 minutes
- **Carousel**: Multiple images with text overlays

### Twitter/X
- **Single tweet**: Quick tip, hot take, link
- **Thread**: Deep dive, tutorial, narrative (3-15 tweets)
- **Reply chain**: Conversation-style engagement
- **Poll**: 2-4 option polling for engagement
- **Spaces**: Live audio discussions

### Instagram
- **Feed post**: Image/video + caption, 150-500 words
- **Carousel**: Multiple images with text overlays
- **Reels**: Short-form video, 15-60 seconds
- **Stories**: Ephemeral content with stickers/polls
- **Live**: Real-time engagement

## Content Calendar Structure

### Weekly Distribution
| Platform | Posts/Week | Content Types |
|----------|-----------|---------------|
| LinkedIn | 3-5 | 2 posts, 1 article/doc, 1 engagement |
| Twitter/X | 5-10 | 3-5 single, 1-2 threads |
| Instagram | 3-5 | 2 feed, 1 reel, 2 stories |

### Calendar Format
```markdown
# Content Calendar: [Week of Date]

## Monday
| Time | Platform | Content Type | Topic | Status |
|------|----------|--------------|-------|--------|
| 8am | LinkedIn | Single Post | [Topic] | Ready |
| 6pm | Instagram | Story | [Topic] | Ready |

## Tuesday
...

## Week Theme: [Theme Name]
## Focus Hashtags: [#tag1, #tag2, #tag3]
```

## Engagement Optimization

### Hook Formulas
- **Pain point**: "Stop doing [X]. Do this instead."
- **Question**: "Did you know that [X]?"
- **Bold statement**: "[Contrarian take that challenges status quo]"
- **Statistic**: "[X]% of [audience] don't [Y]"
- **Story lead**: "I made [mistake]. Here's what happened."

### CTA Types
- **Engagement**: "What's your take?" / "Comment below"
- **Share**: "Tag someone who needs to see this"
- **Save**: "Save this for later"
- **Link click**: "Link in bio to learn more"

## Quality Gates

- Every post MUST have a hook in first line
- Every post MUST have a CTA (engagement, share, or link)
- LinkedIn posts over 300 words get lower engagement
- Twitter threads need standalone-readable tweets
- Instagram captions need hook in first 2 lines

## Output

### Deliverables
- `SOCIAL-CONTENT.md`: All content pieces formatted for each platform
- `CONTENT-CALENDAR.md`: Organized by week/date
- `ENGAGEMENT-PLAN.md`: Hooks and CTAs for each post

### Output Format
```markdown
# Social Content: [Week/Month]

## LinkedIn

### [Post Title]
**Platform:** LinkedIn
**Type:** Single Post / Document / Article
**Topic:** [From topic calendar]
**Date:** [Scheduled date]
**Time:** [Scheduled time]

**Content:**
[Full post copy]

**Hashtags:** #[tag1] #[tag2] #[tag3]
**Link:** [If applicable]
**Status:** Ready / Needs Review

---

## Twitter/X

### [Thread Title]
**Platform:** Twitter/X
**Type:** Thread / Single Tweet
**Topic:** [From topic calendar]
**Date:** [Scheduled date]
**Time:** [Scheduled time]

**Tweet 1:**
[Hook tweet content]
(XX chars)

**Tweet 2:**
[Content tweet]
(XX chars)

**Tweet N:**
[CTA tweet]
(XX chars)

**Hashtags:** #[tag1] #[tag2]
**Status:** Ready / Needs Review

---

## Instagram

### [Post Title]
**Platform:** Instagram
**Type:** Feed / Reel / Story / Carousel
**Topic:** [From topic calendar]
**Date:** [Scheduled date]
**Time:** [Scheduled time]

**Visual:** [Description of image/video]
**Caption:**
[Full caption]

**Hashtags:** #[tag1] #[tag2] #[tag3]
**Status:** Ready / Needs Review

---
```
