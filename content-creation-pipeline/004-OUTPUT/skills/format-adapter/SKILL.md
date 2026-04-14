---
name: format-adapter
description: "Content format adaptation for social media platforms. Transforms base content into platform-specific formats, character limits, and structural requirements. Use when user says adapt content, format for platform, platform format, or format copy."
user-invokable: false
---

# Format Adapter

## Process

1. **Read source content**: get copy deck and content calendar
2. **Identify target platform**: LinkedIn, Twitter/X, or Instagram
3. **Read references**: load `content-creation-pipeline/004-OUTPUT/skills/format-adapter/references/platform-specs.md`
4. **Transform content**: adapt to platform format requirements
5. **Enforce character limits**: validate all copy against limits
6. **Optimize structure**: apply platform-specific formatting
7. **Output formatted content**: ready-to-publish content per platform

## Platform Format Requirements

### LinkedIn Format Specs
| Content Type | Format | Requirements |
|-------------|--------|--------------|
| Single Post | Text + Image | 150-300 words, hook first |
| Document Post | PDF carousel | 10-15 slides, text per slide |
| Article | Long-form | H2 headers, 1,500-3,000 words |
| Video | Native video | Up to 10 min, captions required |

### Twitter/X Format Specs
| Content Type | Format | Requirements |
|-------------|--------|--------------|
| Single Tweet | Text | 280 chars max, hook first 90 |
| Thread | Multi-tweet | 3-15 tweets, standalone-readable |
| Poll | 2-4 options | Question in tweet, options in replies |

### Instagram Format Specs
| Content Type | Format | Requirements |
|-------------|--------|--------------|
| Feed Post | Image/Video + Caption | 150-500 chars, hook first 2 lines |
| Reel | Video | 15-60 sec, hook first 3 sec |
| Story | Image/Video | 15 sec max per frame |
| Carousel | Multi-image | Up to 10 slides, text overlay |

## Transformation Rules

### LinkedIn Transformation
- Expand short copy into conversational tone
- Add professional context and insights
- Use paragraphs (not bullet points)
- Include relevant hashtags at end
- Add first-comment context for document posts

### Twitter/X Transformation
- Tighten copy: every word must earn its place
- Replace complex words with simpler alternatives
- Remove all unnecessary adjectives
- Embed hashtags mid-tweet or at end
- Add threading for multi-thought content

### Instagram Transformation
- Shorten hook to first 2 lines (before "...more")
- Add line breaks for readability (short paragraphs)
- Include 3-5 relevant hashtags in caption or first comment
- Add emoji as visual anchors (sparingly)
- End with engagement question

## Format Checklist

### Pre-Publication Validation
- [ ] Character count verified for platform
- [ ] Hook is in first line (not hidden)
- [ ] CTA is present and actionable
- [ ] Hashtags are relevant and not excessive
- [ ] Links are formatted correctly
- [ ] Tags (@mentions) are correct
- [ ] Image/video specs are met

## Cross-Platform Adaptation

### LinkedIn → Twitter
1. Strip to core message
2. Remove professional jargon
3. Add contrarian hook angle
4. Tighten to 280 chars
5. Add 1-2 relevant hashtags

### LinkedIn → Instagram
1. Lead with visual hook
2. Simplify message to 150 chars first
3. Add line breaks for mobile readability
4. Add 3-5 relevant hashtags
5. End with engagement CTA

### Twitter → LinkedIn
1. Expand single tweet into paragraph
2. Add professional framing
3. Include supporting insight
4. Add relevant hashtags
5. Structure with short paragraphs

## Output

### Deliverables
- `FORMATTED-CONTENT.md`: All content formatted per platform
- Platform-specific files if requested
- Pre-publication checklist per piece

### Output Format
```markdown
# Formatted Content: [Topic/Campaign]

## LinkedIn

### [Title]
**Type:** Single Post / Document / Article
**Word Count:** [XXX] / 300 (optimal)

**Formatted Content:**
[Full formatted post]

**Pre-Publish Checklist:**
- [x] Hook in first line
- [x] CTA present
- [x] Hashtags relevant
- [x] Character count OK

---

## Twitter/X

### [Title]
**Type:** Single Tweet / Thread
**Character Count:** [XXX] / 280

**Formatted Content:**
[Full formatted content]

**Pre-Publish Checklist:**
- [x] Hook in first 90 chars
- [x] CTA present
- [x] Hashtags embedded
- [x] Character count OK

---

## Instagram

### [Title]
**Type:** Feed / Reel / Story / Carousel
**Character Count:** [XXX] / 2,200

**Formatted Content:**
[Full formatted caption]

**Pre-Publish Checklist:**
- [x] Hook in first 2 lines
- [x] CTA present
- [x] Hashtags relevant (3-5)
- [x] Line breaks for readability
- [x] Character count OK
```
