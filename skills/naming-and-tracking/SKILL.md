---
name: naming-and-tracking
description: Stage 0 of the lifecycle pipeline. Generate a campaign's name, registry slug and full UTM set from config before anything is built. Use when starting any new or renewed campaign.
---

# Skill: naming-and-tracking

Assign the campaign's name, registry slug, and full UTM set — **before anything is built**. This is stage 0 of the pipeline: a campaign that isn't trackable by construction never reaches the build stages.

## Why this is a pipeline stage, not documentation

Naming and UTMs fail when they're guidelines someone is supposed to remember. Here they're generated artifacts: the skill produces them from config, downstream skills consume them, and QA rejects any link that doesn't match. Attribution becomes a `GROUP BY`, not a cleanup project.

## Inputs

- The approved brief's one-liner (from `campaign-design`) — or, for a renewal, the existing registry row
- `config/naming-utm.yaml` — the closed vocabularies: team prefixes, motions, audiences, utm_source/utm_medium values

## Output: `tracking/{registry-slug}.md`

```
CAMPAIGN NAME:   [GRW Lifecycle] Adopt Auto-Replies | SMB | V1
REGISTRY SLUG:   grw-lifecycle_adopt-auto-replies_smb_v1

UTM SET (one per link placement):
  base:        utm_source=customer-io & utm_medium=email & utm_campaign=grw-lifecycle_adopt-auto-replies_smb_v1
  email-1 CTA: base + utm_content=email-1_cta-primary
  email-1 footer: base + utm_content=email-1_footer-link
  email-2 CTA: base + utm_content=email-2_cta-primary
  ...

DASHBOARD JOIN KEY: utm_campaign = registry slug  (this is what makes the campaign
visible in the attribution dashboard on day one — see growth-dashboard-spec)
```

## Rules

1. **Every value comes from the config's closed vocabulary.** A motion or source that isn't in `naming-utm.yaml` is a config PR first, a campaign second.
2. **The slug is derived from the name mechanically** (lowercase, `_` between name parts, `-` inside parts) — never hand-written, so name and slug can't drift.
3. **One `utm_content` per link placement**, enumerated up front — the copy skill may only use UTMs listed here.
4. **Renewals bump the version in the name, never rename mid-flight** — historical reporting stays intact; the registry maps old → new.
5. The output file is committed alongside the brief; the QA skill diffs every built link against it.
