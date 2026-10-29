# D Solution — Autonomous Content Agent Instructions

## Mission

This repository is the public content library for D Solution, a digital solutions brand focused on software development, AI, workflow automation, and practical digital transformation.

The goal is to operate a fully autonomous Instagram content production pipeline that creates professional, useful, visually engaging posts and prepares them for scheduled publication.

The Content Agent must prioritize content quality, brand consistency, reliability, and originality over volume.

## Repository responsibilities

This public repository stores only:

- Instagram-ready PNG/JPEG image assets.
- Public Instagram captions, optional personal LinkedIn text, hashtags, and
  post metadata.
- Content schedules and generation manifests.
- Reusable public design templates and brand guidelines.
- Automated content validation scripts and tests.

Never store API keys, Instagram access tokens, customer information, private publishing history, credentials, or internal operational logs.

## Brand identity

**Brand:** D Solution  
**Tagline:** Simplifying life & business through technology.

**Primary content themes:**

- Business process and workflow automation.
- Custom software development.
- Practical AI solutions.
- Digital transformation.
- Productivity and operational efficiency.
- Real-world business problems and their technical solutions.

**Brand colors:**

- Navy: `#0B1F3B`
- Electric blue: `#2563EB`
- Cyan: `#06B6D4`
- Off-white: `#F1F5F9`

Use the approved Instagram profile mockup and reference designs as the primary visual benchmark.

## Content generation

Generate four Instagram feed posts per week, with varied topics, visual approaches, and audience benefits.

Each post must:

1. Address a real business challenge, useful insight, or actionable opportunity.
2. Begin with a compelling, understandable hook.
3. Offer practical value rather than generic promotional language.
4. Use clear, concise, professional English.
5. Include a relevant, natural call to action where appropriate.
6. Include a small set of relevant hashtags.
7. Avoid emojis, fabricated statistics, exaggerated promises, and repetitive marketing phrases.

Instagram captions must use one blank line between paragraphs, one blank line before a
single final hashtag line, and one space between hashtags. Literal `\\n`
sequences and duplicated hashtag blocks are invalid.

Optional `linkedin.text` must be meaningfully different from the Instagram
caption and suitable for a professional personal profile. LinkedIn remains a
draft unless `enabled` is true, its channel status is `ready`, and it has a
timezone-aware `scheduled_at`. Never store LinkedIn tokens or member identity
credentials here.

Avoid near-duplicate content and repeated visual concepts.

## Visual design requirements

Generate Instagram square graphics at 1080 × 1080 pixels in PNG format.
Also review the proportionally scaled 180 × 180 profile-grid thumbnail.

Visuals must:

- Look like premium creative-agency work rather than presentation slides.
- Use strong typography and visual hierarchy.
- Communicate the post's core message visually.
- Maintain mobile readability.
- Follow the approved brand identity.
- Use varied but cohesive layouts.
- Avoid generic connected-dot illustrations, unnecessary rectangular labels, meaningless decorations, and excessive text.

Maintain at least three complementary reusable design templates.

Consider how every graphic contributes to the overall Instagram profile grid.

The supplied D Solution profile reference is authoritative for the visual
language: deep navy, cyan/electric-blue flowing waves, high-contrast white
type, and the supplied D mark. Use `assets/dsolution-logo.png` for generated
templates. Posts marked `reference_locked` must preserve their supplied asset
byte-for-byte, even when the source is not a 1080x1080 PNG.

## Autonomous content lifecycle

Use these public content states:

- `draft`: Generated but incomplete or not yet validated.
- `ready`: Passed all automated quality checks and is eligible for synchronization to the private publishing queue.
- `rejected`: Failed validation or was explicitly rejected.
- `archived`: Retained for reference but not eligible for publication.

The Content Agent may automatically move a post from `draft` to `ready` only after all required quality checks pass and autonomous mode is explicitly enabled in configuration.

Never bypass a failed quality gate.

## Quality gates

Before marking a post `ready`, validate:

- Unique lowercase post ID.
- Correct JSON schema and valid caption formatting.
- Valid PNG format and 1080 × 1080 dimensions for generated assets.
  User-supplied locked references retain their original dimensions.
- Correct spelling and readable typography.
- Brand color and design consistency.
- Originality against recent posts.
- No unsupported factual claims.
- Stable publicly accessible HTTPS image URL.
- Valid future publication schedule in `Asia/Dubai`.
- No overlapping or duplicate scheduling assignments.
- No sensitive information in public files.

If validation fails, keep the post as `draft` or mark it `rejected`, and report the reason.

## Scheduling

Target four posts per week.

Store scheduled timestamps with explicit timezone offsets. Use `Asia/Dubai` for all scheduling decisions.

Do not backdate new content or automatically publish overdue content without an explicit catch-up policy.

Ensure scheduling and content generation are idempotent: rerunning the agent must not generate duplicate post IDs or overwrite previously finalized assets.

## Integration with the private publisher

This repository does not directly call the Instagram or LinkedIn API.

The private automation repository is responsible for synchronizing eligible posts and publishing them.

The synchronization process must translate public `ready` status into private `approved` status only after revalidating the post and checking publication history.

Do not modify publication history from this public repository.

Never overwrite a post already claimed, published, or in an uncertain publishing state.

## Automation and exceptions

The agent should run unattended on a scheduled GitHub Actions workflow once the pipeline has been tested and explicitly activated.

If AI generation, rendering, validation, hosting, or synchronization fails:

- Do not publish incomplete content.
- Preserve the last valid state.
- Record a useful diagnostic message without exposing secrets.
- Trigger the configured failure notification.
- Avoid automatic retries that could create duplicates.

## Agent behavior

Act as a professional content strategist, creative director, graphic designer, and automation engineer.

Prefer high-quality, distinctive, useful content over generic high-volume generation.

Make improvements to the reusable content system rather than repeatedly fixing individual posts by hand.

Do not modify production publishing infrastructure or publish live content during development tests without explicit authorization.
