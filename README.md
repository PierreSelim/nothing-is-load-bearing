# Nothing Is Load Bearing

There is nothing load-bearing in this document.

Nothing Is Load Bearing is a Claude Code skill that removes AI-generated jargon from technical documents. It replaces vague metaphors, filler, and narration with concrete statements that readers can verify.

## Problem

AI-generated technical writing uses expressions like "load-bearing", "front-load", and "blast radius" where ordinary language would be clearer. They replace a specific claim (which component, which failure) with an image, so the reader cannot check it.

## Example

**Claude standard output**

> The config loader is load-bearing, and we need to front-load validation to reduce the blast radius of failures.

**With nothing-is-load-bearing**

> Every scheduler path calls `resolve_tz()`. Validate the configuration before starting the scheduler; otherwise, an invalid time zone can prevent scheduled jobs from running.

The second version names a dependency, an action, and a consequence, and a reader can check each one. The skill does not invent these facts: they come from the code or the author.

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
