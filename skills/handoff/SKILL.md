---
name: handoff
description: Compact the current conversation into a handoff note for another agent to pick up, or load one into this conversation.
argument-hint: "\"load\" to pick one up, or what the next session will be used for"
disable-model-invocation: true
---

If the first argument is `load`, load a handoff (below). Otherwise, write one.

## Write

Write a handoff note summarising the current conversation so a fresh agent can continue the work. Save it through the Obsidian connector as `areas/dev/agents/handoffs/<yyyy-mm-dd-hhmm>-<slug>.md`, with the current working directory as `source` in its frontmatter. Finish by giving the user the note's path.

Include a "suggested skills" section in the note, naming which skills the next agent should call the Skill tool for.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead. The next agent may start on another machine or in another directory, so flag any reference to temp files or uncommitted work.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information, since the vault syncs and keeps its git history.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the note accordingly.

## Load

List `areas/dev/agents/handoffs/`. Take the note the user's remaining arguments describe; with no arguments, take the only note. When more than one note fits, list them with their `source` and ask the user which.

Read the note and every artifact it references. Check each claim that is cheap to check (git state, the files and branches it names), then report a summary of the work, the next step, and every claim that did not hold or could not be checked.

Once the user's reply shows the report matched what they expected, for example by acting on the next step or settling something it raised, delete the note and tell them you did.
