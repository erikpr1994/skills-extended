---
name: upstream-issue-triage
description: Triage open and closed issues plus discussions on the upstream mattpocock/skills repo against our fork, recording a verdict for each so we never re-analyse the same item twice. Use when the user wants to review upstream issues, find patches to pull into the fork, or sync the issue triage log.
metadata:
  internal: true
---

# Upstream issue triage

Repo-only skill. It lives in this repo's `.claude/skills/` so Claude Code auto-loads
it whenever you work in skills-extended. It is kept out of `plugin.json`'s `skills`
array **and** marked `metadata.internal: true` in its frontmatter — the `skills` CLI
scans `.claude/skills/` directly, so the manifest omission alone is not enough; the
`internal` flag is what hides it from `npx skills add` (it stays installable only with
`INSTALL_INTERNAL_SKILLS=1`). It keeps [`LOG.md`](./LOG.md)
— the durable record of every upstream issue and discussion we've already looked at
and what we decided. The point is **incremental**: each run only triages items not
already in the log, so the work compounds instead of repeating.

`LOG.md` has three tracks: an **Issues** track (`## Full triage`, open issues), a
**Discussions** track (`## Discussions`), and a **Closed upstream** track
(`## Closed upstream`, closed issues). All use the same verdict vocabulary. Discussions
skew to `watch`/`skip` — they're mostly ideas without a repro, and Q&A / Show-and-tell /
Announcements rarely imply a fork change — so don't expect many to reach `implement`.
The Closed track skews to `skip`: `COMPLETED`-closed issues reach our fork through
`git rebase upstream/main`, so re-triaging re-derives code we already inherit;
`NOT_PLANNED`-closed (Matt declined) is the one bucket with fork value.

Verdicts: **new** (synced, not yet deliberated), **done** (resolved in our fork),
**implement** (decided to fix, not yet done), **watch** (good idea, but needs design
or upstream may ship it), **skip** (not relevant — other tools/platforms, pure
discussion, packaging we don't need). A row is **resolved** when its verdict is
`done` or `skip`; everything else (`new`, `implement`, `watch`) is **unresolved**
and stays in the backlog.

There are two flows. Pick by what the user asks for — "sync"/"reconcile"/"check for
new issues" → Flow 1; "review an issue"/"pick one"/"what should I fix" → Flow 2. If
the user just runs the skill with no steer, ask which one.

## Flow 1 — Sync the list

Pure list maintenance. No per-item deliberation, no code changes.

1. **Pull items.** Open issues: `gh issue list --repo mattpocock/skills --state open --limit 100 --json number,title`. Closed issues: `gh issue list --repo mattpocock/skills --state closed --limit 500 --json number,title,stateReason`. Discussions: `gh api graphql -f query='{ repository(owner:"mattpocock",name:"skills"){ discussions(first:100,orderBy:{field:UPDATED_AT,direction:DESC}){ nodes{ number title category{name} closed } } } }'`.
2. **Reconcile against [`LOG.md`](./LOG.md):**
   - Any open issue not in `## Full triage` → append a row with verdict `new` and a
     one-line title. Any open discussion not in `## Discussions` → same, noting its
     category. Don't deliberate yet; that's Flow 2.
   - Any closed issue not in `## Closed upstream` → append a row with verdict `new`
     (not pre-judged — the user decides each in Flow 2), its `R` (`C`=COMPLETED /
     `NP`=NOT_PLANNED), and a factual one-line note for context (likely arrives via
     rebase, dup, area). Don't mark it `skip` here.
   - Any logged row in `## Full triage` whose issue is no longer open upstream → move
     it to `## Closed upstream` with verdict `new`, preserving any prior decision in
     the note. (A logged discussion that closed upstream → note it closed.)
3. **Update `Last synced`** to the highest issue number seen and today's date.
4. **Report** the delta: how many new (open issues, closed issues, discussions), how
   many moved to closed, and the new unresolved count. Don't propose fixes here.

## Flow 2 — Review one issue

1. **Pick one unresolved item at random** from any track — `## Full triage`,
   `## Discussions`, or `## Closed upstream` (verdict `new`, `implement`, or `watch`).
   Vary the choice across runs — don't always start from the top, and don't always pick
   open issues over discussions or closed ones. If none are unresolved, say so and
   suggest Flow 1.
2. **Study it.** Read its body (for a discussion, `gh api graphql` its body and
   comments; for a closed issue, read it and any closing comment — `COMPLETED` usually
   means Matt shipped a fix we'll inherit via rebase, so check whether our fork already
   has it before proposing anything), map it to a skill we actually have (see
   `plugin.json` + the bucket READMEs — items about skills/tools we don't ship are an
   immediate `skip`), and grep the target skill to check whether our fork already
   handles it — half of upstream's asks land here independently.
3. **Explain and recommend.** Briefly: what the issue reports, which skill it
   touches, whether our fork already handles it, whether it's worth fixing, and your
   recommended verdict with a one-line rationale.
4. **Ask the user to decide.** Wait for the answer — don't pre-empt it.
   - **Fix** → make the change, verify it (grep/run the repro if there is one),
     record the row as `done`.
   - **Discard / defer** → record `skip` or `watch` with the reason.
5. **Record.** Update the item's row in its track (and the candidates table if a
   `done` issue). Then stop — one item per run, unless the user asks for another.

## Keep the fork philosophy

Per `CLAUDE.md`, this fork is "upstream plus my patches" and the diff stays small.
Favour `implement` only for well-scoped, low-conflict changes. When something is
genuinely useful upstream too, note that it should be filed there.

When a Flow 2 fix edits one of Matt's skills, **match that skill's voice** — mirror
its density and its use (or non-use) of bold, parentheticals, and em-dashes rather
than imposing a house style. Some skills (`diagnose`, `triage`) lean on bold
lead-ins; others (`grill-me`, `handoff`) use none. Add the minimum prose that
conveys the instruction; don't bloat the skill or restate rationale.
