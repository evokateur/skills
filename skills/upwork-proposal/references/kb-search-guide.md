
# KB Search Guide

## Overview

The RAG knowledge base contains project documentation derived from written
sources — git history, code ownership, file structure, and authored notes.
It reflects only what has been documented, not the full scope of the user's
experience. If a search returns weak results for something the user knows they
have experience with, ask before declaring a gap.

## Score Interpretation

- **≥ 0.70** — reliably on-topic, use with confidence
- **0.65–0.70** — borderline, read carefully before citing
- **< 0.65** — treat with skepticism; may be tangentially related or noise

## Query Strategy

**Specific combined queries outperform broad single terms.**

Good: `"WordPress plugin PHP integration"`
Poor: `"WordPress"`

Good: `"ACH file generation NACHA payment processing"`
Poor: `"payments"`

**Lead with the noun that names the capability**, followed by the technology
or domain context. Avoid verbs and generic qualifiers.

## Recommended Search Pattern

For each proposal, run 2–4 searches:

1. **Primary domain search** — the core capability the posting asks for
   (e.g. `"REST API third-party integration PHP"`)

2. **WordPress/platform search** — if the posting names a specific platform
   (e.g. `"WordPress plugin Symfony integration"`)

3. **Secondary skills** — other named requirements
   (e.g. `"OAuth authentication middleware"`)

4. **Gap verification** — if a gap is suspected, search for it before
   declaring it (e.g. `"Vue.js frontend"` to confirm absence)

## Project Source Files

Key project documents in the KB (for reference when interpreting results):

- `projects/eibofli.md` — Symfony + WordPress portal, benefits administration
- `projects/empty-wordpress.md` — WordPress project template, WP-CLI, Composer
- `projects/zenith.md` — Multi-tenant Laravel benefits API
- `projects/natremit.md` — National remittance processing, ACH generation
- `projects/remiton.md` — Remittance portal, ACH, legacy SQL Server
- `projects/ibew701.md` — Union management system, Symfony, financial logic
- `projects/lineco-api.md` — Symfony API Platform, legacy DB integration
- `projects/ctww-api.md` — Laravel API, Auth0, HealthSparq integration
- `projects/bacportal.md` — Union portal, dual-database architecture
- `projects/bac-api.md` — Slim Framework REST API, mobile backend

## Caution: KB Accuracy

Project write-ups should be treated as documentation, not ground truth.
Incidental dependencies (e.g. a package pulled in transitively) may appear
in KB results without reflecting genuine expertise. If a result seems
surprising, verify with the user before citing it in the proposal.

A confirmed hallucination (Vue.js in one project write-up) has been flagged —
treat any frontend framework mentions with particular skepticism unless
the user confirms.
