---
name: nothing-is-load-bearing
description: Removes Claude-flavored jargon from technical writing — analyses, reports, specifications, design docs, software architecture, RFCs, ADRs, postmortems, READMEs, PR descriptions, commit messages. Replaces dead metaphors ("load-bearing", "blast radius", "front-load", "cross-cutting", "fan-out", "gate", "surface area", "heavy lifting", "first-class", "table stakes", "guardrails", "sharp edges") with the concrete claim they stood in for, deletes filler ("it's worth noting", "crucially", "at its core"), and deletes narration, where the text describes what it is about to say instead of saying it ("this section explains", "let's walk through"). Protects genuine terms of art. Use whenever the user asks to write, review, edit, or tighten a technical document, asks for writing that is plainer, less fluffy, less buzzwordy, or less LLM-sounding, says a document "sounds like AI wrote it", or mentions jargon, buzzwords, metaphors, filler, or clichés. Also apply it to your own technical documents before handing them over.
---

# Nothing Is Load Bearing

## Why this matters

A metaphor is a claim the writer has not made yet.

"The config loader is load-bearing" names nobody who depends on the loader and
nothing that breaks if it changes. The reader cannot verify it, act on it, or
disagree with it. Replacing the metaphor with its referent forces the writer to
find out:

> Every scheduler path calls `resolve_tz()`. Changing its signature breaks all
> four callers, including the retry loop that has no test.

That version can be checked and argued with. The point is not style policing but
a check that the document asserts things instead of gesturing at them.

## The test

Apply three questions to each suspicious phrase, in order.

**1. Does the term have a precise definition in this document's domain, shared
by its readers?** In a message-broker specification, *fan-out* names a delivery
topology and *backpressure* names a real mechanism; both stay. In "the fan-out
of this decision across teams", the same word is decoration; it goes.

**2. Can I state the claim with specifics: names, numbers, conditions,
consequences?** If yes, write that instead.

**3. If I delete the phrase, does the sentence lose anything?** If the meaning
survives, the phrase was never saying anything.

## Three things to remove

**Metaphors.** Words borrowed from a domain the document is not about:
construction, war, sport, cooking, plumbing, medicine, theatre. The source
domain is worth knowing: "the foundation is solid, but there is plumbing to do"
is two building metaphors and no engineering.

**Filler.** Phrases that announce or soften a point without making it:
*it is worth noting, crucially, fundamentally, at its core, essentially, truly,
that said, to be clear.* Delete and reread.

**Narration.** Text that talks about the document instead of being it: "This
section describes how retries work", "Let's walk through the flow", "As we will
see", "The following explains", "Below we outline", "In summary", "To recap".
Delete the announcement and start with the content. A heading already says what
a section is about.

> Before: *Migration, in outline:* first the SDK ships, then three things
> follow from that. See below for the rollout.
>
> After: The SDK ships first. Services then onboard in stages, the three with
> the most hard-coded flags first.

Signposts count: "(see below)", "three things follow", "in outline", "the key
steps are". If the next sentence already says it, delete the signpost.

### Metaphors that collide with the document's own subject

A figure of speech borrowed from the domain the document is about causes a
misread, not just a style problem. In a specification that defines `LANDING` as
a milestone, "two legs can land on different partitions" makes the reader check
whether landing logic is involved. Watch for *land, in-flight, takeoff, holding
pattern* in aviation; *settle, clear, balance* in payments; *commit, merge,
branch* in version control; *schedule, queue, block* in operating systems. Use
the plain alternative and keep the technical term for its technical meaning.

### The metaphor moves into the justification

Removing a metaphor relocates the missing claim. "The config loader is
load-bearing" becomes "the config loader is what makes the retry path work", the
same empty assertion in verb form. After the term pass, reread every sentence
that explains why a choice was made. Each should name a mechanism — a call, a
comparison, a stored value, a failure — not just claim importance.

### When you do not know the fact

If a replacement needs a fact you do not have, name the gap in one line and move
on: "Unverified: which callers construct `Flight` directly." Do not invent the
fact to make the sentence concrete, and do not develop the gap into a section.

## Doing the work

**Writing:** use the plain version from the start. Name the module, the caller,
the condition, the number, the failure.

**Reviewing:** scan for the families in `references/jargon-index.md`, then
report a list: quoted phrase, why it is empty, concrete replacement. Do not
silently rewrite someone else's document unless they asked for an edit.

**Editing:** same sections, same order, same scope. A replacement is about as
long as what it replaced, because it says one definite thing.

**Your own draft:** do this every time, without announcing it.

## Replacement patterns

| Instead of | Write the fact |
|---|---|
| X is load-bearing | A, B, and C call X; changing its signature breaks all three |
| the blast radius is large | a failure here stops ingestion and the nightly report; reads keep working |
| front-load the validation | validate on receipt, before the row is written |
| this is a cross-cutting concern | authentication appears in all six handlers |
| gate the rollout on tests | do not deploy until the integration suite passes |
| reduce the surface area of the API | the API exposes 14 public methods; 9 have no external caller |
| the parser does the heavy lifting | the parser resolves aliases, units, and time zones |
| make errors first-class | every operation returns `Result[T, Error]` rather than raising |
| leverage the existing cache | read from the existing cache |
| guardrails prevent misuse | the constructor rejects a landing time earlier than its takeoff |
| there are sharp edges here | two known failure cases: duplicate delivery, and clock skew above 2 s |
| this unlocks future work | with this in place, per-aircraft alerting needs only a new subscriber |
| This section explains how retries work. Retries are... | Retries are... |

## Do not overcorrect

**Terms of art stay.** *Idempotent, at-least-once delivery, backpressure,
circuit breaker, cache, queue, fan-out (in messaging), watermark, race
condition, deadlock, latency, throughput, memory leak, canary release, checksum,
replay, monotonic, eventual consistency.* They have definitions their readers
share.

**Judge each word, not its family.** "Last-write-wins" is an established
conflict-resolution rule and stays; "`ACTUAL` beats `ESTIMATED`" in the same
section is sport, and becomes "takes precedence over".

**The user's own words stay.** If the request says "flaky for months", that is
their fact, not your jargon.

**Do not swap one metaphor for another.** "Ripple effect" for "blast radius"
changes nothing.

**Plain is not vague.** Use concrete verbs — *calls, writes, blocks, retries,
drops, rejects, publishes* — not "handling is performed appropriately".

**Leave quoted material alone.** Jargon inside a quotation, an error message, a
third-party API name, or a cited document stays as written.

## The jargon index

`references/jargon-index.md` lists metaphors grouped by the domain each borrows
from, plus filler, narration, and corporate vocabulary. Read it with the Read
tool when reviewing a document, or when a phrase feels familiar and you want its
replacement.
