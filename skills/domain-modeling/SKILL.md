---
name: domain-modeling
description: Build and sharpen a project's domain model. Use when discussing codebase terminology, writing or editing a project glossary, or recording or editing an ADR.
---

# Domain Modeling

Actively build and sharpen the project's domain model as you design. This is the *active* discipline: challenging terms, inventing edge-case scenarios, and writing the glossary and decisions down the moment they crystallise. (Merely *reading* the glossary for vocabulary is not this skill: that's a one-line habit any skill can do. This skill is for when you're changing the model, not just consuming it.)

## Where the model lives

The domain model lives in the Obsidian vault, not the repo. Read and write it through the Obsidian connector.

```
projects/<project>/
├── glossary
├── adr/
│   ├── 0001-event-sourced-orders
│   └── 0002-postgres-for-write-model
└── llm-context/
```

`<project>` is the git repo root's path relative to `~/code/` (find the root with `git rev-parse --show-toplevel`): `~/code/mattpocock/skills` maps to `projects/mattpocock/skills`. If the repo is outside `~/code/`, ask the user. If `projects/<project>/` doesn't exist in the vault, confirm with the user before creating it.

Note names are lower kebab-case, following the vault convention.

If a `glossary-map` note exists in `projects/<project>/`, the project has multiple contexts. The map points to where each one lives:

```
projects/<project>/
├── glossary-map
├── adr/                 ← project-wide decisions
├── ordering/
│   ├── glossary
│   └── adr/             ← context-specific decisions
└── billing/
    ├── glossary
    └── adr/
```

Create notes lazily: only when you have something to write. If no `glossary` note exists, create one when the first term is resolved. If no `adr/` folder exists, create it when the first ADR is needed.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in the glossary, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y. Which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account': do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible. Which is right?"

### Update the glossary inline

When a term is resolved, update the glossary right there. Don't batch these up: capture them as they happen. Use the format in [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md).

The glossary should be totally devoid of implementation details. Do not treat the glossary as a spec, a scratch pad, or a repository for implementation decisions. It is a glossary and nothing else.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse**: the cost of changing your mind later is meaningful
2. **Surprising without context**: a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off**: there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR. Use the format in [ADR-FORMAT.md](./ADR-FORMAT.md).
