---
name: "Sticklight UX Writer"
version: "1.0.0"
description: >
  Writes on-brand product copy from scratch for the Sticklight product family — the AI web builder
  and the Pink hosting product. Use this skill whenever someone needs to generate, create, or draft
  UX copy, microcopy, button labels, error messages, empty states, tooltips, onboarding flows, CTAs,
  Chat panel responses, deployment messages, or any user-facing text for Sticklight or Pink.
  Triggers on phrases like: "write copy for", "draft this screen", "help me write", "create copy for",
  "what should this say", "suggest copy", "give me options for". Also triggers when a PRD, screenshot,
  wireframe, or feature description is shared and copy is the expected output. Always use this skill
  over generic writing when Sticklight or Pink product context is present.
author: "Elementor Content Design"
license: "CC-BY-NC-4.0"
entry_point: "prompts/write.txt"
---

# Sticklight UX Writer

A skill for generating on-brand, human-centered product copy for the Sticklight product family from scratch.
Takes any combination of context — text description, screenshot, PRD, wireframe — and produces multiple
copy options per surface, grounded in Sticklight's actual brand guidelines, writing rules, and correct
product terminology. Supports feedback and iteration without losing context.

## What it does

| Capability | Description |
|---|---|
| **Context audit** | Identifies missing information and asks for it before writing |
| **Copy generation** | Produces 3 options per surface: Safe, Brand-Forward, and Concise |
| **Brand alignment** | Applies the correct glossary per product (Sticklight or Pink) and all writing guidelines |
| **Cross-product awareness** | Flags term clashes where Sticklight and Pink use different approved terms for the same concept |
| **Image/screenshot input** | Extracts UI context from uploaded designs or wireframes |
| **PRD input** | Reads feature specs and maps them to copy needs |
| **Iteration** | Accepts structured or casual feedback and refines without starting over |

## Product scope

| Product | Glossary | When to use |
|---|---|---|
| Sticklight | `data/glossary.json` | Builder UI, Workspace, Chat panel, Editor, Plan mode, Skills, Templates |
| Pink | `data/pink-glossary.json` | Hosting setup, Deployment, Environments, Domains, Custom variables, Build |

The writing guidelines and reference files apply to both products.

## Surface areas

Applies correct tone standards per context type — identical surface coverage to the Copy Reviewer:
- Error messages, empty states, onboarding, success states
- CTAs, tooltips, destructive actions, navigation labels
- Chat panel (conversational design), upgrade/pricing copy, settings
- Deployment states, environment management, domain setup (Pink)

## Input types

- Product declaration (`PRODUCT: sticklight` or `PRODUCT: pink`) — required if not clear from context
- Text description of a screen, component, or flow
- Screenshot or wireframe (uploaded image)
- PRD or feature spec (pasted text or document)
- A mix of any of the above

## Output format

For each surface or element:
1. **Safe** — Clear, functional, directly on-brand
2. **Brand-Forward** — Leans into Sticklight's or Pink's voice and personality
3. **Concise** — Tightest version for constrained layouts
4. **Rationale** — Why these choices work; any glossary flags or term-clash notes; recommendation

## Data files

| File | Purpose |
|---|---|
| `data/glossary.json` | 30 Sticklight approved/avoided terms with usage rules |
| `data/pink-glossary.json` | 14 Pink approved/avoided terms with usage rules |
| `data/writing-guidelines.json` | 50 rules: voice, tone, grammar, UX writing, inclusive language |
| `refernce/term-clashes.md` | Cross-product clash reference — terms that differ between products |
| `refernce/calibration.md` | Good/bad copy examples per dimension for output calibration |
| `prompts/write.txt` | Main writing prompt |

> **Setup note:** Data files are shared with the Sticklight Copy Reviewer. Copy them from
> `sticklight-product-copy-reviewer/data/` and `sticklight-product-copy-reviewer/refernce/` into
> this skill's corresponding folders. Keep both skills in sync when glossary or guidelines are updated.

## Scope

- **Single string** — one label, CTA, tooltip, or error message
- **Component** — all strings in one UI component
- **Screen** — full copy across one screen or modal
- **Flow** — end-to-end copy across multiple screens, with cross-screen consistency checks
