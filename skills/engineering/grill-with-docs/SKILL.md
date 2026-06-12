---
name: grill-with-docs
description: Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates documentation (CONTEXT.md, DESIGN.md, ADRs) inline as decisions crystallise. Use when user wants to stress-test a plan against their project's language and documented decisions.
---

<what-to-do>

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by exploring the codebase, explore the codebase instead.

</what-to-do>

<supporting-info>

## Domain awareness

During codebase exploration, also look for existing documentation:

### File structure

Most repos have a single context:

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```
/
├── CONTEXT-MAP.md
├── docs/
│   └── adr/                          ← system-wide decisions
├── src/
│   ├── ordering/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                 ← context-specific decisions
│   └── billing/
│       ├── CONTEXT.md
│       └── docs/adr/
```

Create files lazily — only when you have something to write. If no `CONTEXT.md` exists, create one when the first term is resolved. If no `docs/adr/` exists, create it when the first ADR is needed.

## Design awareness

If the plan touches UI, the visual system has its own glossary: `DESIGN.md`. It is to design what `CONTEXT.md` is to the domain — the settled conventions (color, type, spacing, component inventory, layout patterns), not the reasoning behind them. During exploration, read it if present and challenge the plan against it the same way you do `CONTEXT.md`.

Create `DESIGN.md` lazily — only when the first visual convention is settled. If the repo already keeps a design-system doc, update that instead of inventing your own. Use the format in [DESIGN-FORMAT.md](./DESIGN-FORMAT.md). Keep it to settled conventions — the *why* behind a hard visual decision goes in an ADR, not here.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account' — do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible — which is right?"

### Prototype UI decisions, don't describe them

When a question is spatial — layout, control placement, flow, visual hierarchy, modal-vs-page — text is a poor medium. Generate a minimal throwaway HTML mockup with 2+ variants side by side and let the user react. Delegate the file to a sub-agent so the grilling thread stays focused, then resume with one question: "which variant?" For a richer interactive comparison, hand off to [`prototype`](../prototype/SKILL.md).

Capture the choice before deleting the mockup — it doesn't go in `CONTEXT.md`, which is a glossary, not a design log:

- The **settled convention** goes in `DESIGN.md` ("primary actions live in a sticky bottom bar"), like any resolved term.
- If the choice was a real trade-off worth an ADR, record the *why* there — and paste a screenshot or the variant markup into it first, so the rejected options survive the mockup's deletion.

Then delete the mockup.

### Update CONTEXT.md inline

When a term is resolved, update `CONTEXT.md` right there. Don't batch these up — capture them as they happen. Use the format in [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).

`CONTEXT.md` should be totally devoid of implementation details. Do not treat `CONTEXT.md` as a spec, a scratch pad, or a repository for implementation decisions. It is a glossary and nothing else.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR. Use the format in [ADR-FORMAT.md](./ADR-FORMAT.md).

</supporting-info>
