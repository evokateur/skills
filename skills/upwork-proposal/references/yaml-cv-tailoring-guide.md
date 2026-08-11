
# YAML CV Tailoring Guide

## Purpose

The tailored yaml-cv.md is a posting-specific derivative of the master CV.
It reweights emphasis toward what the posting cares about and away from what
it doesn't. It is not a different CV — it is the same career presented through
a different lens.

## Source

Always derive from the master CV before writing any tailored version:

[[areas/job-search/yaml-cv|Master CV]]

## Primary Levers

These four fields carry most of the tailoring weight:

**`profession`**
Name the role as the posting names it, or close to it. "Backend Developer &
API Integration Specialist" for an integration posting. "Backend Developer"
for a general PHP role. "Software Engineer" only when the posting is senior
and broad.

**`core_expertise`**
Three items, ordered by relevance to the posting. Lead with the domain or
capability the posting centres on. This is the first thing a reader sees after
the name — it should confirm fit immediately.

**`summary_of_qualifications`**
Rewrite for each posting. The master summary is a good skeleton but should
not be used verbatim — the posting-specific summary should foreground the
relevant domain and capabilities, not the full range of the user's experience.
One paragraph, 4–6 sentences.

**`responsibilities` bullets**
The most granular tailoring lever. For each posting:
- Lead with the 2–3 bullets most directly relevant to what the posting asks for
- Amplify: expand or rewrite bullets that speak to the posting's core needs
- Tone down: shorten or remove bullets that are real but off-topic
- Maximum 6–8 bullets; fewer is often better
- Never fabricate — only reweight and reframe what's genuinely there

## Secondary Levers

**`areas_of_expertise`**
Reorder technologies to lead with what the posting names. Remove technologies
not relevant to the posting (e.g. remove FastAPI from a WordPress PHP posting).
Methods & Practices should reflect the posting's language where possible.

**`profession` in `additional_experience`**
Leave untouched — these roles are historical and shouldn't be reframed.

## Amplify / Tone Down Heuristic

For each capability or technology in the posting, ask:
- **Does the user have genuine experience here?** If yes, find the bullets that
  demonstrate it and bring them forward or expand them.
- **Is this a secondary concern of the posting?** If yes, keep but don't lead.
- **Is this irrelevant to the posting?** If yes, remove or shorten to one line.

Never remove a bullet that was added specifically to demonstrate fit for this
posting type. Cut from the generic infrastructure/process bullets first
(e.g. Homestead, Git workflow, GitLab administration) — these are real but
are rarely what a client is hiring for.

## Pagination

If the education section splits across a page break, cut responsibility bullets
— starting from the least relevant to the posting, working inward. Two bullets
removed usually resolves a pagination problem. Never cut WordPress or
domain-specific bullets that motivated the tailoring.

Check with the user before cutting if the tradeoff is not obvious.

## Output Path

    areas/job-search/cv-joint/job-postings/<slug>/yaml-cv.md
