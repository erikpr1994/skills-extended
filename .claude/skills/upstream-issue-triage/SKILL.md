---
name: upstream-issue-triage
description: Triage open issues on the upstream mattpocock/skills repo against our fork, recording a verdict for each so we never re-analyse the same issue twice. Use when the user wants to review upstream issues, find patches to pull into the fork, or sync the issue triage log.
---

# Upstream issue triage

Repo-only skill. It lives in this repo's `.claude/skills/` so Claude Code auto-loads
it whenever you work in skills-extended — but it is **not** in `plugin.json`'s `skills`
array, so `npx skills` never ships it to other projects. It keeps [`LOG.md`](./LOG.md)
— the durable record of every upstream issue and discussion we've already looked at
and what we decided. The point is **incremental**: each run only triages items not
already in the log, so the work compounds instead of repeating.

`LOG.md` has two tracks: an **Issues** track (`## Full triage`) and a **Discussions**
track (`## Discussions`). Both use the same verdict vocabulary. Discussions skew to
`watch`/`skip` — they're mostly ideas without a repro, and Q&A / Show-and-tell /
Announcements rarely imply a fork change — so don't expect many to reach `implement`.

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

1. **Pull open items.** Issues: `gh issue list --repo mattpocock/skills --state open --limit 100 --json number,title`. Discussions: `gh api graphql -f query='{ repository(owner:"mattpocock",name:"skills"){ discussions(first:100,orderBy:{field:UPDATED_AT,direction:DESC}){ nodes{ number title category{name} closed } } } }'`.
2. **Reconcile against [`LOG.md`](./LOG.md):**
   - Any open issue not in `## Full triage` → append a row with verdict `new` and a
     one-line title. Any open discussion not in `## Discussions` → same, noting its
     category. Don't deliberate yet; that's Flow 2.
   - Any logged row whose issue/discussion is no longer open upstream (closed/merged)
     → note it as closed upstream so it drops out of the backlog.
3. **Update `Last synced`** to the highest issue number seen and today's date.
4. **Report** the delta: how many new (issues and discussions), how many now closed
   upstream, and the new unresolved count. Don't propose fixes here.

## Flow 2 — Review one issue

1. **Pick one unresolved item at random** from either track (verdict `new`,
   `implement`, or `watch`). Vary the choice across runs — don't always start from
   the top, and don't always pick issues over discussions. If none are unresolved,
   say so and suggest Flow 1.
2. **Study it.** Read its body (for a discussion, `gh api graphql` its body and
   comments), map it to a skill we actually have (see `plugin.json` + the bucket
   READMEs — items about skills/tools we don't ship are an immediate `skip`), and
   grep the target skill to check whether our fork already handles it — half of
   upstream's asks land here independently.
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
