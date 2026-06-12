# What this repo is

This is a **fork of [`mattpocock/skills`](https://github.com/mattpocock/skills)**, maintained as
[`erikpr1994/skills-extended`](https://github.com/erikpr1994/skills-extended).

**Why it exists:** to ship fixes and improvements on my own timeline instead of waiting for upstream
to accept them. Upstream is actively maintained, so this is *not* a hard divergence — it's "upstream
plus my patches." Whenever something here could help everyone, file it upstream too (e.g. the
prototype-during-grill idea is [mattpocock/skills#336](https://github.com/mattpocock/skills/issues/336))
and link the issue from the commit, so a patch can be dropped once upstream merges its own version.

**Keep the diff small.** Because upstream moves, the cost of this fork is rebase drift. Prefer minimal,
well-scoped changes, rebase onto upstream regularly, and avoid gratuitous reformatting that creates
merge conflicts against `mattpocock/skills`.

## Remotes & syncing

- `origin` → `erikpr1994/skills-extended` (the fork — push here)
- `upstream` → `mattpocock/skills` (Matt's repo — pull here, never push)

```bash
# pull upstream's new work, keep my patches on top
gh repo sync erikpr1994/skills-extended --source mattpocock/skills
git fetch upstream && git rebase upstream/main && git push --force-with-lease origin main
```

## How it's consumed

Other repos install from the fork, not from Matt's:

```bash
npx skills@latest add erikpr1994/skills-extended
npx skills update
```

# Repo conventions

Skills are organized into bucket folders under `skills/`:

- `engineering/` — daily code work
- `productivity/` — daily non-code workflow tools
- `misc/` — kept around but rarely used
- `personal/` — tied to my own setup, not promoted
- `in-progress/` — drafts not yet ready to ship
- `deprecated/` — no longer used

Every skill in `engineering/`, `productivity/`, or `misc/` must have a reference in the top-level `README.md` and an entry in `.claude-plugin/plugin.json`. Skills in `personal/`, `in-progress/`, and `deprecated/` must not appear in either.

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`.

Each bucket folder has a `README.md` that lists every skill in the bucket with a one-line description, with the skill name linked to its `SKILL.md`.
