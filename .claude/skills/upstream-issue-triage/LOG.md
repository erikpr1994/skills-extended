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
| 306 | handoff | Verify-vs-assumed discipline + resume protocol. Ships with a ready-to-pull diff. | ✅ applied (adapted — guarded git/gh block + split into handoff/resume-handoff) |
| 299 | grill-with-docs | ADRs for unimplemented work poison `docs/adr/`. Add a lifecycle/status marker. Erik's area. | open — design |
| 271 | write-a-skill | Reported internal contradiction. Cheap if real. | ✅ applied (500→100 lines, all 3 refs agree) |
| 303 | improve-codebase-architecture | Add progressive-disclosure-of-implementation lens. Fills the AI-navigability gap the skill already advertises. | ✅ applied (LANGUAGE.md principle + SKILL.md explore prompt/benefit) |
| 296 | teach | Tree/hierarchy diagrams mix ASCII chars with inline HTML → alignment breaks in proportional fonts. Real repro w/ screenshot. | ✅ applied (semantic-HTML guidance line in Lessons) |

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
| 312 | add .claude-plugin/marketplace.json | packaging | skip | dup of #21. Would add a native `/plugin install` path for the fork (tiny, low-conflict new file), but duplicates the documented `npx skills add erikpr1994/skills-extended` install story + a 2nd packaging file to keep in sync. Deferred 2026-06-12 — keep single install path for now |
| 311 | grill-me no durable output artifact | grill-me | watch | parallels #337; reuse DESIGN.md idea |
| 310 | to-issues vertical-slice completeness check | to-issues | watch | |
| 309 | teach learning record generated with lesson | teach | watch | |
| 308 | grill-me-with-options for Copilot/VS Code | Copilot | skip | platform we don't use |
| 307 | documentation review & alignment skill | new skill | watch | |
| 306 | handoff verify-vs-assumed + resume protocol | handoff + resume-handoff | done | applied 2026-06-12; adapted contributor diff (nbost130 branch), not verbatim. Two changes vs upstream: (1) guarded the git/gh state-capture block for non-repo handoffs ("what's deployed/running/open"), since our handoff was tool-agnostic; (2) split write vs resume into TWO skills — handoff (write, the tagging discipline) + new resume-handoff (read: drift-check, re-probe [UNVERIFIED], read source of truth). Erik's call: distinct entry points for the two jobs. Diverges structurally from upstream's single-file #306 → higher rebase cost accepted. New skill wired into README + bucket README + plugin.json. Upstream #306 still OPEN (it IS the issue); our split is fork-specific, not for upstream |
| 303 | progressive-disclosure architecture lens | improve-codebase-architecture | done | applied 2026-06-12; added principle to LANGUAGE.md (framed complementary to "depth is a property of the interface" — internal disclosure for maintainers/agents, guarded by deletion test), explore prompt + benefit term to SKILL.md. Upstream #303 still OPEN/unanswered — file there too |
| 301 | block-dangerous-git bypassed by git global opts | git-guardrails | done | applied 2026-06-12; repro tests pass |
| 299 | grill-with-docs ADRs for unimplemented work | grill-with-docs | implement | open; needs status/lifecycle marker |
| 298 | canonical-name label sets need no mapping | setup/triage | skip | niche |
| 297 | deferred state role for trigger-gated work | triage | watch | relates to #139/#289 |
| 296 | teach tree/hierarchy diagrams in explainers | teach | done | applied 2026-06-12; added a tree/hierarchy guidance line to teach Lessons section (semantic nested-list HTML, not ASCII; if ASCII, wrap in `<pre><code>`, never mix tree chars with inline styling). Real repro w/ screenshot upstream. Upstream #296 still OPEN — file there too |
| 294 | grill-with-docs docs location outside worktree | grill-with-docs | watch | cross-worktree; Erik's area |
| 292 | to-issues parent pickable after decomposition | to-issues | watch | |
| 290 | improve-arch HTML pages need handoff button | improve-codebase-architecture | watch | |
| 289 | triage home for dormant defect w/ reactivation | triage | watch | relates to #139/#297 |
| 286 | teach code-highlight feature | teach | watch | |
| 274 | improve-arch worse after grill-me added | improve-codebase-architecture | watch | core grievance (single solution → immediate grill) already designed out in our fork: step 2 presents a candidate shotgun as HTML report then asks "Which of these would you like to explore?" (SKILL.md:71); grilling (step 3) is gated behind an explicit pick (SKILL.md:73-75). Reporter hit older upstream version. Residual grill-volume concern is model-dependent (comments split on 4.6 vs 4.8) + user can decline — not worth a patch now |
| 272 | handoff temp-location issues on Windows | handoff | skip | we're on macOS |
| 271 | contradiction in write-a-skill | write-a-skill | done | applied — SKILL.md:18 said 500 lines, split rule + checklist say 100; aligned to 100. File upstream too |
| 269 | DEEPENING→LANGUAGE dependency propagation | ubiquitous-language (deprecated) | skip | deprecated skill |
| 268 | add skills to Cursor Marketplace | Cursor | skip | platform |
| 265 | to-issues implicit interface blockers | to-issues | watch | |
| 263 | review jumps to fixing after review | review (in-progress) | watch | "jumps to fixing" grievance is moot in our fork: our `review` draft is read-only two-axis (Standards/Spec) reporter, never edits code (SKILL.md:67-71). Inline-PR-comment want unsupported in draft, but native `/code-review --comment` already covers that workflow. Our review is in-progress/internal (unshipped) — PR-comment mode is speculative scope for now |
| 262 | relationship to GitHub issues | triage/to-issues | watch | |
| 254 | sh-script skill selector | orchestrator | skip | overlaps #197/#252 |
| 252 | skill-router skill | orchestrator | watch | |
| 243 | remove deprecated qa mention in setup | setup-matt-pocock-skills | done | applied 2026-06-12; dropped `qa` from issue-tracker explainer (SKILL.md:38). Upstream #243 still OPEN (mention still on upstream/main); we patched ahead — reporter's proposed fix is 3113779 on their fork, unmerged |
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
| 21 | marketplace.json for plugin marketplace | packaging | skip | identical ask to #312 — deferred together 2026-06-12 (keep single `npx skills add` install path) |

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
| 293 | /grill-with-docs to state progress | Ideas | done | progress was the symptom; real gap = untracked design tree. Added `### Track the design tree` (throwaway `.grill-tree.md`) to grill-with-docs. Filed upstream as issue #338 |
| 288 | README 'Putting it together' lifecycle section | Ideas | watch | good idea but blocked on Matt's design answer (canonical sequence vs toolbox; where ongoing-maintenance skills sit) — proposer deliberately deferred. README is a hot, rebase-expensive upstream file; new narrative section costs drift for docs-only benefit. Skill-level seam already patched (#287); relates to #241 |
| 287 | improve-arch end-state: hand off or stop at ADRs? | Q&A | watch | gap verified in fork (step 3 documented reject side effect but not accept). Patched: added accepted-candidate terminal-state bullet to SKILL.md step 3 — loop ends at design+docs; offer handoff to `/to-issues` or `/tdd`. Verdict kept `watch`: unanswered upstream Q&A, realign if Matt's intended design differs. File upstream too |
| 285 | how does it compare to openspec / spec frameworks | Q&A | new | |
| 275 | grill-with-docs with multilingual application | General | new | |
| 270 | writing skills and prompts with TypeScript | Ideas | skip | external tool promotion (mantiq — github.com/webNeat/mantiq): author's own CLI+skill for prompts-as-TypeScript. No concrete change to a skill we ship; prompts-as-code cuts against the repo's model-agnostic markdown-skill design |
| 267 | featured on Locally Hosted (video) | Show and tell | new | |
| 261 | proposal: codehealth-mcp skill | Ideas | new | |
| 259 | what mode should I run grill-me in? | Q&A | skip | answered Q&A; grill-me is a mode-agnostic prep instruction — no fork change |
| 257 | can /superpowers be complementary? | General | new | |
| 256 | explore code with subagent in /grill-me | Ideas | done | line 10 already explored-instead-of-asked; added "prefer a subagent so exploration doesn't clutter this conversation" (portable, no Explore hardcode). File upstream too |
| 255 | GitHub Copilot as a supported agent | General | new | platform; likely skip |
| 248 | anyone tried Claude's rules feature? | Q&A | new | |
| 246 | /write-a-skill vs Anthropic's /skill-creator | General | skip | opinion thread, no comments/repro/proposed change. Asks Matt why he wrote his own vs Anthropic's heavier skill-creator (bundles /agents, /scripts). Our write-a-skill already covers scripts + reference files (SKILL.md steps 1-2); Anthropic's skill-creator is separately installable for anyone wanting the heavier tool. Adopting its architecture cuts against the repo's minimal-markdown-skill design |
| 239 | using curated subsets of skills from plugin | Ideas | new | |
| 236 | nightshift: autonomous to-prd→to-issues layer | Show and tell | new | |
| 231 | how to manage high-level roadmaps? | Q&A | new | |
| 226 | technical design docs in AI workflow | General | new | |
| 225 | how do you work across multiple repos? | General | new | |
| 217 | PRD lifecycle after all issues implemented | General | new | |
| 214 | Welcome to Discussions! | Announcements | new | skip on review |
