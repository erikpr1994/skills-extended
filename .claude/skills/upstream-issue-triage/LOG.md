# Upstream issue triage log

Durable record of `mattpocock/skills` open issues and discussions we've analysed, so
we never re-triage the same item. Maintained by the [`upstream-issue-triage`](./SKILL.md)
skill (Flow 1 syncs new items as `new`; Flow 2 reviews one unresolved item).
Verdicts: **new** · **done** · **implement** · **watch** · **skip**. Resolved =
`done`/`skip`; unresolved (still in the backlog) = `new`/`implement`/`watch`.
Issues live in `## Full triage`; discussions in `## Discussions`.

**Last synced:** issues #337, discussions #333 — 2026-06-12

## Implement candidates

High-confidence, cheap patches to skills we use. The first four were applied
2026-06-12 (commit on `main`); the rest are still open.

| # | Skill | Why | Status |
|---|---|---|---|
| 301 | git-guardrails-claude-code | `git -C`/`-c`/`--git-dir` slips past `block-dangerous-git.sh` — every guard bypassed. Security. | ✅ applied (normalize + 8 repro tests pass) |
| 335 | teach | Correct answer always same position (A). Vary position + plausible distractors. | ✅ applied |
| 240 | grill-me | Agent jumps to implementation when questions run out. Stop + ask for next step. | ✅ applied |
| 221 | grill-with-docs | "One question at a time" ignored — strengthen enforcement. | ✅ applied |
| 306 | handoff | Verify-vs-assumed discipline + resume protocol. Ships with a ready-to-pull diff. | open — review diff |
| 299 | grill-with-docs | ADRs for unimplemented work poison `docs/adr/`. Add a lifecycle/status marker. Erik's area. | open — design |
| 271 | write-a-skill | Reported internal contradiction. Cheap if real. | ✅ applied (500→100 lines, all 3 refs agree) |

## Full triage

| # | Title (short) | Skill / area | Verdict | Note |
|---|---|---|---|---|
| 337 | grill-with-docs prototype docs home (DESIGN.md) | grill-with-docs | done | Erik filed; shipped in fork (DESIGN.md) |
| 336 | grill-with-docs prototype UI decision points | grill-with-docs | done | Erik filed; shipped in fork |
| 335 | teach quiz answer-position tell | teach | done | applied 2026-06-12 |
| 332 | teach lesson-to-lesson nav buttons | teach | watch | QoL; needs index.html scheme |
| 329 | run triage + tdd agents automatically | triage/tdd | watch | orchestration; larger design |
| 328 | to-issues handoff-ready issues (stories+notes) | to-issues | watch | |
| 324 | coordinating multiple team members | discussion | skip | no concrete skill change |
| 323 | prd-to-issues configurable detail level | to-prd/to-issues | watch | cost-control knob |
| 321 | bounded-context CONTEXT.md sub-domains | grill-with-docs | watch | open question |
| 320 | teach Tailwind v4 CDN instead of hand CSS | teach | watch | token win; cross-session consistency |
| 317 | teach token reduction (shared CSS + compaction) | teach | watch | overlaps #320 |
| 316 | teach quiz answer-length tell | teach | done | fixed at teach SKILL.md:101 |
| 312 | add .claude-plugin/marketplace.json | packaging | watch | could ease fork install; dup of #21 |
| 311 | grill-me no durable output artifact | grill-me | watch | parallels #337; reuse DESIGN.md idea |
| 310 | to-issues vertical-slice completeness check | to-issues | watch | |
| 309 | teach learning record generated with lesson | teach | watch | |
| 308 | grill-me-with-options for Copilot/VS Code | Copilot | skip | platform we don't use |
| 307 | documentation review & alignment skill | new skill | watch | |
| 306 | handoff verify-vs-assumed + resume protocol | handoff | implement | open; ready diff in issue |
| 303 | progressive-disclosure architecture lens | improve-codebase-architecture | watch | |
| 301 | block-dangerous-git bypassed by git global opts | git-guardrails | done | applied 2026-06-12; repro tests pass |
| 299 | grill-with-docs ADRs for unimplemented work | grill-with-docs | implement | open; needs status/lifecycle marker |
| 298 | canonical-name label sets need no mapping | setup/triage | skip | niche |
| 297 | deferred state role for trigger-gated work | triage | watch | relates to #139/#289 |
| 296 | teach tree/hierarchy diagrams in explainers | teach | watch | |
| 294 | grill-with-docs docs location outside worktree | grill-with-docs | watch | cross-worktree; Erik's area |
| 292 | to-issues parent pickable after decomposition | to-issues | watch | |
| 290 | improve-arch HTML pages need handoff button | improve-codebase-architecture | watch | |
| 289 | triage home for dormant defect w/ reactivation | triage | watch | relates to #139/#297 |
| 286 | teach code-highlight feature | teach | watch | |
| 274 | improve-arch worse after grill-me added | improve-codebase-architecture | watch | real regression report; relevant |
| 272 | handoff temp-location issues on Windows | handoff | skip | we're on macOS |
| 271 | contradiction in write-a-skill | write-a-skill | done | applied — SKILL.md:18 said 500 lines, split rule + checklist say 100; aligned to 100. File upstream too |
| 269 | DEEPENING→LANGUAGE dependency propagation | ubiquitous-language (deprecated) | skip | deprecated skill |
| 268 | add skills to Cursor Marketplace | Cursor | skip | platform |
| 265 | to-issues implicit interface blockers | to-issues | watch | |
| 263 | review jumps to fixing after review | review (in-progress) | watch | wants PR-comment mode |
| 262 | relationship to GitHub issues | triage/to-issues | watch | |
| 254 | sh-script skill selector | orchestrator | skip | overlaps #197/#252 |
| 252 | skill-router skill | orchestrator | watch | |
| 243 | remove deprecated qa mention in setup | setup-matt-pocock-skills | watch | cheap cleanup; check our copy |
| 242 | setup scaffold a skill-usage guide | setup-matt-pocock-skills | watch | |
| 241 | README clarify handoff parallel-branching | handoff/README | watch | |
| 240 | grill-me jumps to implementation | grill-me | done | applied 2026-06-12 |
| 238 | to-issues wave milestones for exec order | to-issues | watch | |
| 235 | handoff persisting/tracking ideas | handoff | watch | overlaps #306 |
| 229 | /write-commit skill | new skill | watch | |
| 221 | grill-with-docs one-question-at-a-time ignored | grill-with-docs | done | applied 2026-06-12 |
| 210 | /ce-compound knowledge-codify skill | new skill | watch | |
| 207 | GLOSSARY.md vs CONTEXT.md naming | naming | skip | discussion |
| 200 | triage duplicate acceptance criteria | triage/to-issues | skip | verified: doesn't reproduce — triage keeps AC only in Agent Brief comment, to-issues only in `## Acceptance criteria`; no combined template |
| 197 | skill orchestrator for choosing workflows | orchestrator | watch | recurring theme |
| 196 | update installed skills when source changes | packaging | watch | relevant to fork-sync UX |
| 188 | /visualize-architecture skill | new skill | watch | |
| 180 | improve-arch module secrets & connascence | improve-codebase-architecture | watch | |
| 170 | make this a valid npm package | packaging | skip | |
| 163 | Codex OpenAI metadata on manual skills | Codex | skip | platform |
| 162 | /help <intent> skill recommender | orchestrator | watch | overlaps #197/#252 |
| 147 | GitHub releases for changes | packaging | skip | |
| 145 | lightweight /prototype-with-docs | prototype/grill-with-docs | watch | Erik already did prototype-during-grill |
| 139 | "blocked" sixth triage state | triage | watch | relates to #289/#297 |
| 138 | individually-installable plugins (tdd) | packaging | skip | |
| 133 | extensions / agent-rules-books integration | packaging | skip | |
| 132 | light improvement to grill-with-docs | grill-with-docs | watch | vague; Erik's area |
| 130 | Codex treats CONTEXT.md as PRD/plan | grill-with-docs | watch | |
| 129 | tdd issues have no memory of each other | tdd | watch | overlaps #49 |
| 124 | user confirmation checkpoint Phase 4→5 | tdd/to-issues | watch | |
| 116 | support Beads issue tracker | triage/to-issues | skip | tool we don't use |
| 114 | code review skill | review (in-progress) | watch | we have review draft |
| 113 | skills only in CLI, not Desktop | platform | skip | |
| 49 | to-issue picked up via /tdd | to-issues/tdd | watch | overlaps #129/#329 |
| 47 | to-issues native sub-issues not body refs | to-issues | watch | |
| 45 | enforce numbered questions per question | grill | watch | overlaps #221 |
| 23 | "the flow" | discussion | skip | |
| 21 | marketplace.json for plugin marketplace | packaging | watch | dup of #312 |

## Discussions

Open `mattpocock/skills` discussions. Same verdicts; skewed to `watch`/`skip` since
most are ideas without a repro and Q&A / Show-and-tell / Announcements rarely imply a
fork change. Seeded 2026-06-12 (all `new`, not yet deliberated — that's Flow 2).

| # | Title (short) | Category | Verdict | Note |
|---|---|---|---|---|
| 333 | to-prd (was write-a-prd) doesn't interview | Q&A | new | |
| 331 | mobile-first dashboard for /teach workspaces | Ideas | new | |
| 322 | nice combination: /teach & /grill-me | Show and tell | new | |
| 315 | making docs accessible to everyone in company | Q&A | new | |
| 314 | /teach need knowledge/reference setup? | Q&A | new | |
| 313 | /teach: some related, complementary skills | Ideas | new | |
| 304 | naming grill-with-docs skill | General | new | |
| 302 | CONTEXT-MAP.md ADRs issue? | General | new | relates to #299 |
| 300 | plan-and-execute: 'how' layer after grill→prd→issues | Show and tell | new | |
| 293 | /grill-with-docs to state progress | Ideas | new | relates to #311/#337 |
| 288 | README 'Putting it together' lifecycle section | Ideas | new | |
| 287 | improve-arch end-state: hand off or stop at ADRs? | Q&A | new | improve-codebase-architecture area |
| 285 | how does it compare to openspec / spec frameworks | Q&A | new | |
| 275 | grill-with-docs with multilingual application | General | new | |
| 270 | writing skills and prompts with TypeScript | Ideas | new | |
| 267 | featured on Locally Hosted (video) | Show and tell | new | |
| 261 | proposal: codehealth-mcp skill | Ideas | new | |
| 259 | what mode should I run grill-me in? | Q&A | new | |
| 257 | can /superpowers be complementary? | General | new | |
| 256 | explore code with subagent in /grill-me | Ideas | new | |
| 255 | GitHub Copilot as a supported agent | General | new | platform; likely skip |
| 248 | anyone tried Claude's rules feature? | Q&A | new | |
| 246 | /write-a-skill vs Anthropic's /skill-creator | General | new | |
| 239 | using curated subsets of skills from plugin | Ideas | new | |
| 236 | nightshift: autonomous to-prd→to-issues layer | Show and tell | new | |
| 231 | how to manage high-level roadmaps? | Q&A | new | |
| 226 | technical design docs in AI workflow | General | new | |
| 225 | how do you work across multiple repos? | General | new | |
| 217 | PRD lifecycle after all issues implemented | General | new | |
| 214 | Welcome to Discussions! | Announcements | new | skip on review |
