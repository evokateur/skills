---
name: upwork-proposal
description: >-
  Use when the user wants to plan, draft, or iterate on a proposal for an Upwork
  job posting. The user will reference a posting by URI (e.g.
  `job-postings/cat-butt`), which corresponds to a folder under
  `areas/job-search/cv-joint/` in the vault. Produces a `proposal-notes.md`
  artifact through collaborative iteration, drawing on KB project research and
  the user's master CV.
---

# Upwork Proposal Skill

## Situation

The user is a backend developer (Wesley Hinkle) building a freelance presence
on Upwork. For each job posting they want to apply to, the goal is to produce
an effective proposal — one that honestly represents their experience, leads
with the strongest evidence of fit, and is calibrated to the specific posting
rather than generic.

The user will give a URI in the form of `job-postings/<identifier>`

Job posting notes will be in the Obsidian vault under:

    areas/job-search/cv-joint/<uri>

The vault directory contains some or all of:

- `job-posting.md` — a structured analysis of the posting, produced by an
  agent based on the original job posting content. Useful as a checklist of
  extracted requirements and keywords.
- `content.md` — **the original job posting text.** May be more reliable
  than the LLM generated structured analysis.

The user's experience is documented in a RAG knowledge base of project write-ups.
The KB reflects only what has been documented — it is not exhaustive. The user
may have relevant experience not yet captured there.

## Goal

Produce a `proposal-notes.md` note in the posting directory — a plan document
the user can reference while filling out the Upwork proposal form. The note is
the artifact of a collaborative planning conversation, not the output of an
autonomous generation pipeline.

The note should contain (see `references/proposal-notes-template.md`):

- **Key Points** — positioning rationale, primary differentiator, tone, rate
  strategy if applicable, budget/scope anomaly and milestone strategy if
  applicable
- **Relevant Projects** — drawn from KB research, with specific detail mapping
  each project's capabilities to the posting's requirements
- **Form and Content of Cover Letter** — structural decisions and paragraph
  shape
- **Cover Letter Draft** — flowing prose, written to the rules in
  `references/cover-letter-guide.md`

A tailored **yaml-cv.md** may also be produced if the user wants one.
The note `areas/job-search/yaml-cv.md` contains the base CV.

    Write to: areas/job-search/cv-joint/job-postings/<identifier>/yaml-cv.md

See `references/yaml-cv-tailoring-guide.md` for field-by-field guidance.

## On Loading This Skill

When invoked with `/upwork-proposal <uri>`, do the following before responding:

1. **List the posting directory** to see which input files are present:
   `obsidian:list_directory → areas/job-search/cv-joint/job-postings/<identifier>/`

2. **Read the posting files** — `content.md` first, then `job-posting.md` if
   present. Read both the [[areas/job-search/yaml-cv|master CV]] and the
   [[geekpay-laravel-backend-developer/proposal-notes|GeekPay tone reference]].

3. **Search the KB** for relevant projects using requirements drawn from
   `content.md` as the primary source, cross-referenced against
   `job-posting.md`. Run 2–4 searches. See `references/kb-search-guide.md`
   for query strategy and score interpretation.

4. **Generate a tentative draft** of the proposal-notes note — your best
   current read of the positioning, relevant projects, and cover letter shape,
   based on what you've read. Make it concrete and specific; the user will
   steer from here. Flag anything uncertain or requiring user confirmation
   rather than glossing over it.

The conversation that follows is the planning process. Update the note
iteratively as the user gives feedback. Always read the current note before
writing to it.

## Key Principles

**content.md is ground truth.** When the structured analysis in job-posting.md
conflicts with or adds to what's in content.md, flag it rather than accepting
it silently.

**The KB is not exhaustive.** Weak search results don't mean a gap exists —
ask the user before declaring one. Verify surprising results (especially
frontend framework mentions) before citing them.

**Honest gaps, handled well.** A gap that is load-bearing for the role should
be acknowledged in the cover letter in a way that strengthens rather than
weakens the candidacy (see GeekPay as the canonical example). Minor gaps are
usually better left unmentioned.

**The cover letter is not a CV summary.** It makes an argument; the CV provides
evidence. Flowing prose, no bullets or headers, formal register. See
`references/cover-letter-guide.md`.

**Milestone strategy belongs in the terms field.** If the posting has a budget
anomaly or vague scope, a discovery milestone is often the right approach —
but that framing goes in Upwork's dedicated terms field, not the cover letter.

## Reference Files

Load as needed — not all at once:

- `references/proposal-notes-template.md` — canonical structure for the artifact
- `references/cover-letter-guide.md` — form rules, structure, what goes where
- `references/yaml-cv-tailoring-guide.md` — field-by-field CV tailoring logic
- `references/kb-search-guide.md` — RAG query strategies and score guidance
