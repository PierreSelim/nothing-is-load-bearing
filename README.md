# Nothing Is Load Bearing

There is nothing load-bearing in this document.

Nothing Is Load Bearing is a Claude Code skill that removes AI-generated jargon from technical documents. It replaces vague metaphors, filler, and narration with concrete statements that readers can verify.

## Problem

AI-generated technical writing uses expressions like "load-bearing", "front-load", and "blast radius" where ordinary language would be clearer. They replace a specific claim (which component, which failure) with an image, so the reader cannot check it.

## Example

Prompt: a design-review note on how message retries affect a specification for a system that tracks aircraft delays from pub/sub messages, written in a metaphor-heavy register.

**Claude standard output**

> Retry safety is load-bearing on §3.2's strict "newer than", the bouncer that turns duplicates away. Remove it and the blast radius of one stale message ripples through every later milestone.

**With nothing-is-load-bearing**

> Retry safety depends on §3.2, which rejects a redelivered message because its `event_time` is not newer than the stored one. Without it, a stale estimate overwrites a newer one and §3.5 copies the wrong delay to the later milestones, giving up to four wrong delays.

The second version names the rule, what it does, and the consequence, so a reader can check each against the specification. The skill does not invent these facts: they come from the code, the specification, or the author.

## What it does

- Replaces empty metaphors such as "load-bearing", "blast radius", and "heavy lifting" with the facts behind them.
- Deletes filler and narration such as "it is worth noting", "let's walk through", and "as we will see".
- Requires concrete claims that name the components, conditions, mechanisms, and consequences involved.
- Keeps technical terms such as "idempotency", "backpressure", and "eventual consistency" when they have a precise meaning in context.
- Never invents evidence. When a concrete replacement needs information that is unavailable, it names the gap.

## Scope

Use the skill when writing, reviewing, or editing technical material, including:

- Architecture and design documents
- Architecture Decision Records (ADRs) and RFCs
- Technical reports, investigations, and postmortems
- READMEs and internal documentation
- Pull request descriptions and commit messages
- Technical analyses and specifications

It works both on new drafts and on documents assembled from existing documentation or multiple contributors.

## Installation

This repository is a Claude Code plugin with its own marketplace. In Claude Code:

```
/plugin marketplace add PierreSelim/nothing-is-load-bearing
/plugin install nothing-is-load-bearing@nothing-is-load-bearing
```

To try it from a local clone without installing:

```sh
claude --plugin-dir /path/to/nothing-is-load-bearing
```

### Manual install

Without the plugin, copy the skill directory into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project):

```sh
cp -r skills/nothing-is-load-bearing ~/.claude/skills/
```

The skill includes `references/jargon-index.md`, which lists over 400 metaphors, grouped by the domain each one borrows from, with what to write instead. The skill reads it when reviewing a document.

## Usage

Claude loads the skill when a request matches its description: writing, reviewing, or editing technical documents. You can also invoke it directly.

### Plain-English requests

Ask Claude to:

- "Remove the AI jargon from this document."
- "Review this ADR for readability."
- "Rewrite this section in natural technical English."

### Slash command

Invoke the skill by name to apply it to a document or passage:

- Installed as a plugin: `/nothing-is-load-bearing:nothing-is-load-bearing`
- Installed manually: `/nothing-is-load-bearing`

## License

MIT. See [LICENSE](LICENSE).
