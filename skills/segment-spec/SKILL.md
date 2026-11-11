---
name: segment-spec
description: Stage 2 of the lifecycle pipeline. Turn an approved brief's audience into an exact, layered segment definition (baseline AND excludes AND campaign logic). Use before building any audience in a CRM/ESP.
---

# Skill: segment-spec

Turn a brief's audience section into an exact, layered segment definition ready to build in any CRM/ESP.

## Input

An approved brief from `campaign-design` (its Audience + Segment sketch sections).

## Output: `segments/{registry-slug}.md`

```
SEGMENT: {registry-slug}

LAYER 0 — BASELINE (mandatory, never modified here):
  master_eligibility_baseline        # active + deliverable + not opted out + not protected

LAYER 1 — ALWAYS-EXCLUDES (list each, with reason):
  NOT excl_active-sales-cycle        # open opportunity — sales owns the conversation
  NOT excl_onboarding                # guided onboarding window

LAYER 2 — CAMPAIGN LOGIC:
  has_feature_x = false
  AND automation_rate < 0.14
  AND plan_tier IN ('smb','commercial')

ESTIMATED SIZE: ~N accounts (state the query/source used)
OVERLAP CHECK: list running campaigns sharing >20% of this audience (from registry)
DATA FRESHNESS: for each trait used — where it comes from and how often it syncs
```

## Rules

- **Layer 0 and 1 are imports, not re-implementations.** If the brief asks to bypass the baseline, stop and escalate — that's a policy change, not a segment.
- Every trait must be verified to exist in the data source before speccing (name, type, sync cadence). A segment on a stale or missing trait is the #1 silent killer — I once found half a cohort silently excluded by one broken trait.
- Estimated size must come from an actual count query, not intuition; include the number and the date.
- Flag any trait whose definition depends on another team's pipeline — that's a dependency to document in the registry.
