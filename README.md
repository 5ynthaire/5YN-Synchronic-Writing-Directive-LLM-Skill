# Synchronic Writing Directive For AI Artifact Generation

A framework and skill for writing software artifacts (READMEs, design docs, API references, invariants, comments, specs) as present-state descriptions.

The artifact states what the system *is* and *does*. Justifications refer only to current consequences, invariants, and failure modes. Temporal narrative, change history, and decision chronology are excluded from the primary text.

## Synchronic vs Diachronic

- **Synchronic** — a cross-section of the system as it exists now. Structure and rules are treated as present truth. Relations and consequences that hold *now* supply the justification.
- **Diachronic** — the evolutionary path: “we used to… then… therefore…”, changelogs embedded in the description, version stories, decision history.

Synchronic form reduces token cost for downstream readers (human or model) and removes narrative bias that a fresh instance would otherwise have to discount.

## Rules

1. Present tense, declarative voice.  
   “X handles Y because Z produces race conditions under concurrent load.”

2. Justify only by present consequences, invariants, and failure modes.  
   Never reconstruct the sequence of past decisions.

3. No temporal framing.  
   Avoid or rewrite: “changed from”, “updated”, “previously”, “we decided”, “now supports”, “migrated from”, changelog-style lists inside the main description.

4. History, when required, lives in a clearly labeled separate section or file.  
   The primary artifact remains synchronic.

5. Matter-of-fact tone.  
   No dramatization, journey language, or narrative arc.

6. Preserve technical precision.  
   Names, signatures, constraints, edge cases, and examples stay exact; only framing and tense change.

## Skill

The skill `synchronic-prose` implements the rules above. Invoke it by requesting artifacts “in synchronic prose”, “as present-state description”, or “strip the narrative/history”.

```
---
name: synchronic-prose
description: Write or rewrite coding artifacts, READMEs, design docs, specs, invariants, APIs, and similar materials in pure synchronic prose. Use when the user wants matter-of-fact present-state descriptions free of change history, temporal narrative, decision chronology, or dramatized progression. Triggers include synchronic, atemporal, present-state docs, clean artifacts, no changelog narrative, strip history from README or design doc.
---

# Synchronic Prose

Write and edit artifacts so they describe the current system as a self-contained fact. Eliminate diachronic framing.

## The Distinction

- **Synchronic** — cross-section of the system as it exists now. Structure, rules, interfaces, and invariants are stated as present truth. Justifications refer only to current consequences and relations.
- **Diachronic** — evolutionary path, change logs, "we used to… then… therefore…", decision history, temporal narrative. Exclude this from the artifact body.

New readers or model instances receive a clean picture with minimal narrative weight or temporal noise.

## Rules for Writing and Editing

1. **Present tense, declarative voice.** State what the system *is* and *does*. Prefer "X handles Y because Z produces race conditions under concurrent load" over any story of how the choice was reached.

2. **Justify by present consequences only.** Scaffold with current problems, invariants, failure modes, and internal relations. Never reconstruct the sequence of past decisions.

3. **No temporal framing.** Ban or rewrite phrases such as:
   - "changed from A to B"
   - "updated", "new in this version", "previously", "we decided", "after evaluating"
   - "latest", "now supports", "migrated from"
   - Change-log style lists inside the main description

4. **Separate history if needed.** If a change log or decision record is required, place it in a distinct section or file explicitly labeled as historical. The primary artifact remains synchronic.

5. **Matter-of-fact tone.** No dramatization, no "journey", no narrative arc. Treat the content the way a well-written law, scientific model, or fictional civilization's governing principles would be presented — as given.

6. **Preserve technical precision.** Keep exact names, signatures, constraints, edge cases, and examples. Only the framing and tense change.

## Editing Workflow

When given existing text:

- Identify and remove or relocate all diachronic material (history, "why we switched", version notes).
- Convert remaining explanations to present-tense justifications grounded in current behavior and constraints.
- Ensure the result stands alone as a complete description of the system *as it is*.

## Examples of the Shift

**Diachronic (undesired):**
> We originally used a simple mutex. Under load this caused contention, so we switched to a lock-free ring buffer. The new design also made it easier to add multiple consumers later.

**Synchronic (desired):**
> The queue is a lock-free ring buffer. A mutex would serialize producers and create contention under concurrent load. The ring-buffer design supports multiple consumers without additional synchronization.

**Diachronic README fragment:**
> v2.3 — Added support for streaming. Previously the API only accepted complete payloads.

**Synchronic equivalent:**
> The API accepts both complete payloads and streaming input. Streaming mode delivers chunks as they arrive and signals end-of-stream with a terminal marker.

## Scope

Apply to READMEs, design documents, API references, invariants, configuration schemas, architectural descriptions, domain rules, and analogous artifacts (including fictional laws or scientific theories presented as current models). Do not force the style onto process tutorials, ADRs, or explicit historical records when those are the requested genre.
```

## Scope

Primary targets: READMEs, design documents, API references, invariants, configuration schemas, architectural descriptions, domain rules, and equivalent artifacts.  

Process tutorials, Architecture Decision Records, and explicit historical records remain outside the primary style when those genres are requested.

## License

[MIT](LICENSE)
