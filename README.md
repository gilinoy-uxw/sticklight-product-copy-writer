# Sticklight UX Writer Skill

An AI-powered product copy writer built for the [Sticklight](https://sticklight.io) product family.

This skill writes on-brand UI copy from scratch for **Sticklight** (the AI web builder) and **Pink** (the hosting and deployment product). It gathers context, generates three distinct options per surface, and iterates on feedback — all grounded in Sticklight's real brand glossary, writing guidelines, and UX best practices.

The companion to the [Sticklight Copy Reviewer](https://github.com/gilinoy-uxw/sticklight-product-copy-reviewer). **Reviewer checks. Writer creates.**

Compatible with **Claude Desktop**, **Claude Code**, **Cursor**, and other compatible tools.

---

## What it does

The Sticklight UX Writer helps writers, designers, and product teams generate on-brand copy for any UI surface across the Sticklight product family.

It:

- Audits context before writing — asks for missing info when needed
- Writes three distinct options per surface: **Safe**, **Brand-Forward**, and **Concise**
- Applies the correct glossary per product (30 Sticklight terms, 14 Pink terms)
- Applies all 50 writing guidelines — flags violations in Rationale, silent improvements go straight into copy
- Flags cross-product term clashes (e.g. "Workspace" means something different in each product)
- Calibrates output quality against the real good/bad examples in `refernce/calibration.md`
- Accepts feedback and iterates without losing context or glossary alignment

---

## Folder structure

```
sticklight-copy-writer/
├── SKILL.md                      # Skill metadata for Claude, Cursor, Codex
├── prompts/
│   └── write.txt                 # Main writing prompt with full generation logic
├── data/
│   ├── glossary.json             # 30 Sticklight approved/avoided terms
│   ├── pink-glossary.json        # 14 Pink approved/avoided terms
│   └── writing-guidelines.json  # 50 rules with reviewer_behavior field
├── refernce/
│   ├── term-clashes.md           # Cross-product clash reference
│   └── calibration.md           # Good/bad copy examples per dimension
└── README.md                    # You're here
```

> **Data files are shared with the Sticklight Copy Reviewer.** When you update a term in `glossary.json` or add a rule to `writing-guidelines.json`, sync the change to the reviewer's `data/` folder too — or vice versa. One source of truth for both skills.

---

## How it works

1. The user declares the product (`PRODUCT: sticklight` or `PRODUCT: pink`) or it's inferred from context.
2. The skill checks for missing context (surface type, audience, constraints) and asks if needed.
3. For each surface, it generates three distinct copy options grounded in the correct glossary and guidelines.
4. The Rationale block explains the choices, flags any avoided-term substitutions, and notes cross-product clashes where relevant.
5. On feedback, it iterates while preserving brand alignment — never starting from scratch unless asked.

---

## Output example

**Empty state — Chat panel, no conversations yet (Sticklight)**

**Option 1 — Safe**
> Your first conversation is one message away.
> Open the Chat panel and describe what you want to build.
> **Start a conversation**

**Option 2 — Brand-Forward**
> This is where your site comes to life.
> Tell Sticklight what you're working on — it'll take it from here.
> **Say something**

**Option 3 — Concise**
> No conversations yet.
> **Start building**

**Rationale**
- Options 1 and 2 frame the empty state as an invitation, not an absence — per `ux-01`.
- "Chat panel" is used throughout per the Sticklight glossary (avoided: "AI panel").
- Option 2 leans into the creator-in-command frame (voice-02) without overpromising.
- Option 3 is for layouts where body copy is truncated.
- **Recommendation:** Option 1 for standard layouts; Option 3 for mobile or collapsed panels.

---

## Getting started

### Use in Claude Desktop

1. Zip the folder
2. Upload via **Settings → Skills → Upload skill**

Then prompt:

```
PRODUCT: sticklight
Write copy for the empty state when a creator has no projects yet.
First-time user. Include heading, body, and CTA.
```

Or attach a screenshot:

```
PRODUCT: pink
[attach screenshot] Write copy for this deployment failure screen.
```

### Use in Claude Code

Move or link the folder into your local skills directory:

```
~/.claude/skills/sticklight-copy-writer/
```

Then trigger it with any copy request that includes Sticklight or Pink context.

---

## Example prompts

**From description (Sticklight):**
```
PRODUCT: sticklight
Write copy for the modal when a creator is about to delete a project.
Deletion is permanent. Audience: experienced creator, solo use.
```

**From description (Pink):**
```
PRODUCT: pink
Write copy for the success state after a creator successfully sets up a custom domain.
First-time setup. They'll be redirected to the Environments overview next.
```

**From a PRD:**
```
PRODUCT: sticklight
[paste PRD section] Write copy for the Plan mode tooltip that appears when a creator
hovers over the mode switcher. 80 character limit.
```

**Iteration:**
```
Option 2 feels right but the CTA is too long. Can you tighten all three?
```

---

## Keeping data in sync

Both skills share the same source of truth. When either glossary or the writing guidelines change:

```
# From reviewer → writer
cp sticklight-product-copy-reviewer/data/glossary.json sticklight-copy-writer/data/
cp sticklight-product-copy-reviewer/data/pink-glossary.json sticklight-copy-writer/data/
cp sticklight-product-copy-reviewer/data/writing-guidelines.json sticklight-copy-writer/data/
cp sticklight-product-copy-reviewer/refernce/term-clashes.md sticklight-copy-writer/refernce/
cp sticklight-product-copy-reviewer/refernce/calibration.md sticklight-copy-writer/refernce/
```

---

## License

Creative Commons Attribution-NonCommercial 4.0 International
© Elementor Ltd., 2025

---

## Contributors

**Elementor Content Design Team**
Built with care for the creators building on Sticklight.
