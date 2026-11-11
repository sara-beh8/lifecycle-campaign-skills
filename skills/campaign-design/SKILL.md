---
name: campaign-design
description: Stage 1 of the lifecycle pipeline. Turn a business goal into a reviewable campaign brief: audience, entry/exit, success metrics, flow sketch. Use when a new campaign is requested or an old one is due for renewal.
---

# Skill: campaign-design

Turn a business goal into a reviewable campaign brief. This is stage 1 of the pipeline — nothing downstream starts without an approved brief.

## Inputs (require all; ask if missing)

- **Goal**: the business outcome ("drive adoption of feature X in segment Y")
- **Audience hypothesis**: who and why now
- **Product context**: current feature list + recent releases (file or URL — never rely on model memory)
- **Constraints**: send-frequency caps, excluded audiences, brand rules

## Output: `briefs/{registry-slug}.md` with exactly these sections

1. **One-liner** — campaign purpose in one sentence
2. **Audience** — who enters, in plain language + estimated size
3. **Entry / exit conditions** — what triggers entry; what ends the journey (conversion event, time, exit segment)
4. **Segment sketch** — baseline + excludes + campaign logic (handed to `segment-spec`)
5. **Flow sketch** — numbered steps (`01 fetch context`, `02 branch first-time?`, ...), max 7 steps for v1
6. **Success metrics** — ONE primary human metric with current baseline and target; guardrail metrics (unsub rate, spam); the conversion goal event that must be configured
7. **Proof points** — which current product facts the copy will use (from product context input, cited)
8. **Risks & open questions** — anything needing a human decision, flagged explicitly

## Rules

- Primary metric must be a **human** metric (human CTOR, conversions) — never machine-inflated opens
- If no conversion goal event can be defined, say so loudly: an unmeasurable campaign is a decision, not an accident
- If the audience overlaps a running campaign (check the registry), surface the overlap in Risks — do not silently proceed
- The brief must name a **review date** — every campaign is born with its renewal scheduled
