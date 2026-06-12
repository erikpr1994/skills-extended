# Upstream issue triage log

Durable record of `mattpocock/skills` open issues and discussions we've analysed, so
we never re-triage the same item. Maintained by the [`upstream-issue-triage`](./SKILL.md)
skill (Flow 1 syncs new items as `new`; Flow 2 reviews one unresolved item).
Verdicts: **new** · **done** · **implement** · **watch** · **skip**. Resolved =
`done`/`skip`; unresolved (still in the backlog) = `new`/`implement`/`watch`.
Open issues live in `## Full triage`; discussions in `## Discussions`; closed issues
in `## Closed upstream` (synced as `new` so each is decided in Flow 2, not pre-judged).

**Last synced:** open issues #337, discussions #333, closed issues swept through #334 — 2026-06-12

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
| 332 | teach lesson-to-lesson nav buttons | teach | watch | QoL; needs index.html scheme — now exists via #331 (DASHBOARD-FORMAT.md). Revisit: dashboard gives a home page but not lesson↔lesson prev/next nav |
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
| 331 | mobile-first dashboard for /teach workspaces | Ideas | done | applied 2026-06-12; added DASHBOARD-FORMAT.md (new root `index.html` home page) + `index.html` workspace-file bullet and "The Dashboard" section to teach SKILL.md. Adapted soymarketing:teach-add-dashboard contributor branch — trimmed to match teach's *-FORMAT.md voice. Docs-only/additive (new file + additive SKILL.md lines), no manifest change. Partly unblocks #332 (lesson nav "needs index.html scheme"). Upstream #331 still OPEN/unanswered (fork PRs disabled) — file/comment upstream too |
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

## Closed upstream

Closed `mattpocock/skills` issues, swept exhaustively so we never wonder "did we miss
a good closed one." **Reason** is the GitHub close reason: `C` = COMPLETED (Matt shipped
it), `NP` = NOT_PLANNED (Matt declined). The **Note** is factual context only — close
reason, whether it likely arrives via `git rebase upstream/main`, duplicates, area — to
speed your decision; it is **not** a verdict.

Every closed row syncs as `new` so you decide each yourself in Flow 2 — nothing here is
pre-judged. Seeded as a one-time full sweep 2026-06-12 (188 items); these rows ARE
selectable in Flow 2, and Flow 1 keeps them current.

| # | R | Title (short) | Skill / area | Verdict | Note |
|---|---|---|---|---|---|
| 334 | C | Re-enable "discovering new skill" | packaging | new | shipped upstream (rebase) |
| 330 | C | how to update synced skills (npx) | packaging | new | usage Q; answered upstream |
| 327 | C | grill-me decision tree + adversarial + summary | grill-me | new | shipped upstream; our grill-me patched via #240 |
| 326 | C | teach quiz feature request | teach | new | shipped upstream (rebase) |
| 325 | C | token-optimized `-condensed` skill variants | packaging/all | new | relates #320/#317 teach-token; revisit for fork take |
| 319 | C | PRD: Skill Trace 引擎 | demo PRD | new | generated/demo PRD |
| 318 | C | install command unusable UI | packaging | new | shipped upstream (rebase) |
| 305 | C | support persisted design decisions | grill-with-docs | new | shipped upstream; relates our #306/#293 design-tree |
| 295 | C | add AskQuestion tool | grill | new | shipped upstream (rebase) |
| 284 | C | grill-with-docs output frequency | grill-with-docs | new | shipped upstream; our #221 covers |
| 283 | C | policy: no verify/check mode for setup | setup | new | upstream policy decision |
| 282 | C | policy: no hard question limits grilling | grill | new | upstream policy; aligns our #45/#221 |
| 281 | C | policy: issue trackers mainstream only | triage/to-issues | new | upstream policy |
| 280 | C | ship /writing-shape | writing | new | shipped upstream (rebase) |
| 279 | C | ship /writing-fragments | writing | new | shipped upstream (rebase) |
| 278 | C | ship /writing-beats | writing | new | shipped upstream (rebase) |
| 277 | C | ship /teach | teach | new | shipped upstream (we ship it) |
| 276 | C | ship /review | review | new | shipped upstream (rebase) |
| 273 | C | improve-arch mention severity | improve-codebase-architecture | new | shipped upstream (rebase) |
| 266 | C | grill-with-docs CONTEXT-FORMAT Rules stale | grill-with-docs | new | shipped upstream (rebase) |
| 264 | C | takeover skill (mirrors handoff) | handoff | new | relates our handoff/resume-handoff split; revisit for fork take |
| 260 | C | codehealth-mcp skill | MCP | new | MCP tool we don't ship (open dup #261 watch) |
| 253 | C | add BitBucket git host | setup | new | shipped upstream (rebase) |
| 251 | C | antigravity harness support | platform | new | platform we don't use |
| 250 | C | grill-with-context use most capable model | grill-with-docs | new | shipped upstream (rebase) |
| 249 | C | grill-me-store-decisions persists decision tree | grill-me | new | relates our #306/#293/#311; revisit for fork take |
| 247 | C | severity of grill-me/grill-with-docs | grill | new | shipped upstream (rebase) |
| 245 | C | dedicated /code-review skill | review | new | shipped upstream; native /code-review covers (#114/#263) |
| 244 | C | grill-with-docs challenge premise first | grill-with-docs | new | shipped upstream (rebase) |
| 237 | C | /domain-model referenced in docs | docs | new | shipped upstream (rebase) |
| 234 | C | Kiro IDE symlink copies | platform | new | platform we don't use |
| 233 | C | feedback/analytics for skills | meta | new | discussion; nothing to ship |
| 232 | C | improve-arch continues implementation | improve-codebase-architecture | new | shipped upstream; our #274 verified designed-out |
| 230 | C | to-issues GH CLI problem | to-issues | new | shipped upstream (rebase) |
| 228 | C | custom link dir for other agents | packaging | new | shipped upstream (rebase) |
| 227 | C | change how to deal with old issue | unclear | new | unclear/noise |
| 224 | C | technical design docs in AI workflow | discussion | new | dup of disc #226 |
| 223 | C | . | — | new | noise |
| 222 | C | typo README ticks→tickets | README | new | shipped upstream (rebase) |
| 220 | C | stealth install option for setup | setup | new | shipped upstream (rebase) |
| 219 | C | formatting for the grill | grill | new | shipped upstream (rebase) |
| 218 | C | PRD: sub-pi agent dispatch & worktree | demo PRD | new | generated/demo PRD |
| 216 | C | link-skills.sh readlink -f macOS | packaging | new | shipped upstream (rebase) |
| 215 | C | handoff empty temp file Windows | handoff | new | Windows; our #272 skip (macOS) |
| 213 | C | enable Discussions | meta | new | repo admin |
| 212 | C | PRD lifecycle after issues | discussion | new | dup disc #217 |
| 211 | C | mktemp XXXXXX placeholder | handoff | new | shipped upstream (rebase) |
| 209 | C | Meldefrist in Admin-Tabelle | — | new | noise (no context) |
| 208 | C | grill-me remove codebase-specific guidance | grill-me | new | shipped upstream (rebase) |
| 206 | C | update deprecated mktemp in handoff | handoff | new | shipped upstream (rebase) |
| 205 | C | to-issues without triage artifacts | to-issues | new | shipped upstream (rebase) |
| 204 | C | add skills to existing repo | packaging | new | usage Q |
| 203 | C | CLI-backed local issue tracker | triage/to-issues | new | shipped upstream (rebase) |
| 202 | C | Co-Work env / other harnesses | platform | new | platform |
| 201 | C | handoff skill suggestion | handoff | new | shipped upstream (rebase) |
| 199 | C | grill-with-docs default English | grill-with-docs | new | shipped upstream (rebase) |
| 198 | C | grill-with-docs default English (dup) | grill-with-docs | new | dup of 199 |
| 195 | C | function/where applied | Q | new | usage Q |
| 194 | C | cli doesn't recognize skills | support | new | support |
| 193 | C | some security issues to check | security | new | shipped upstream (rebase) |
| 192 | C | grill-me use askUserQuestion | grill-me | new | shipped upstream (rebase) |
| 191 | C | /mainline git-native intent memory | new skill | new | shipped/declined upstream (rebase) |
| 190 | C | CONTEXT.md grows too large | grill-with-docs | new | shipped upstream; relates our #293 tree |
| 189 | C | caveman wenyan intensity levels | caveman | new | skill we don't promote |
| 187 | C | handoff flagged high risk by synk | handoff | new | scanner false positive |
| 186 | C | handoff loses load-bearing decisions | handoff | new | shipped upstream; our #306 covers |
| 185 | C | grill-with-docs reach for askUserQuestion | grill-with-docs | new | shipped upstream (rebase) |
| 184 | C | gh auth token | support | new | support |
| 183 | C | ctx recommendation integration | orchestrator | new | shipped/declined; relates #197 |
| 182 | C | grill-with-docs alignment before questions | grill-with-docs | new | shipped upstream (rebase) |
| 181 | C | /extract-context skill | new skill | new | shipped upstream (rebase) |
| 179 | C | ISO 8601 file names | handoff/naming | new | shipped upstream (rebase) |
| 178 | C | Codex version? | platform | new | platform |
| 177 | C | Gitea issue-tracker support | setup | new | shipped upstream (rebase) |
| 176 | C | community translations README | README | new | shipped upstream (rebase) |
| 175 | C | mktemp BSD macOS | handoff | new | shipped upstream (rebase) |
| 174 | C | .claude folder missing fresh install | packaging | new | shipped upstream (rebase) |
| 173 | C | slices: main agent or subagents | tdd/to-issues | new | shipped upstream (rebase) |
| 172 | C | descriptive handoff filenames | handoff | new | shipped upstream (rebase) |
| 171 | C | secret redaction handoff | handoff | new | shipped upstream (rebase) |
| 169 | C | dedicated prd label | to-prd | new | shipped upstream (rebase) |
| 168 | C | grill-with-docs prevent AskUserQuestion | grill-with-docs | new | shipped upstream (rebase) |
| 167 | C | docs refine prototype wording | docs | new | shipped upstream (rebase) |
| 166 | C | domain-model missing from package | packaging | new | deprecated skill |
| 165 | C | grill-with-docs + copilot graph api | platform | new | platform |
| 164 | C | 4 misc skills missing from plugin.json | packaging | new | shipped upstream; our plugin.json maintained |
| 161 | C | Defender malicious report | security | new | false positive |
| 160 | C | Disregard: Error | — | new | noise |
| 159 | C | skills-manifest + per-skill CHANGELOG | packaging | new | shipped/declined upstream |
| 158 | C | /verify skill pre-commit | verify | new | shipped upstream (we have verify) |
| 157 | C | caveman output style vs skill | caveman | new | skill we don't promote |
| 156 | C | to-prd not apply ready-for-agent | to-prd | new | shipped upstream (rebase) |
| 155 | C | grill with docs output as file | grill-with-docs | new | shipped upstream; relates our #337/#293 |
| 154 | C | prime AGENTS.md/CLAUDE.md re CONTEXT.md | grill-with-docs | new | shipped upstream (rebase) |
| 153 | C | grill-me/grill-with-docs open-ended | grill | new | shipped upstream (rebase) |
| 152 | C | tech debt | — | new | noise |
| 151 | C | idea | — | new | noise |
| 150 | C | grep flag parsing `--` patterns | tooling | new | shipped upstream (rebase) |
| 149 | C | prevent grill-with-docs askUserQuestion | grill-with-docs | new | dup of 168 |
| 148 | C | priority-score to-prd/to-issues | to-prd/to-issues | new | shipped upstream (rebase) |
| 146 | C | .agent folder windows | platform | new | platform |
| 144 | C | caveman internal monologue | caveman | new | skill we don't promote |
| 143 | C | review skills - here's what i got | feedback | new | feedback thread |
| 142 | C | gh CLI command-shape in setup | setup | new | shipped upstream; our #243 area |
| 141 | C | managed dotfiles symlink | packaging | new | shipped upstream (rebase) |
| 140 | C | wrong dest dir installing Claude Code | packaging | new | shipped upstream (rebase) |
| 136 | C | issue-tracker-gitlab `--state` invalid | setup | new | shipped upstream (rebase) |
| 134 | C | grill-with-docs implements after grill | grill-with-docs | new | shipped upstream; our #221/#240 cover |
| 131 | C | contextive for context | grill-with-docs | new | external tool |
| 128 | C | skip needs-triage after to-prd→to-issue | triage/to-issues | new | shipped upstream (rebase) |
| 127 | C | ADRs different name to avoid LLM bias | grill-with-docs | new | shipped upstream; relates our #299/disc #302 |
| 126 | C | Spanish version proposal | i18n | new | shipped/declined upstream |
| 125 | C | rolling question queue grill-with-docs | grill-with-docs | new | shipped upstream; relates our #293 |
| 123 | C | grill-me-with-docs explicit subagent | grill-with-docs | new | shipped upstream; relates disc #256 |
| 122 | C | better direct opencode support | platform | new | platform |
| 121 | C | slash-commands not showing | support | new | support |
| 120 | C | setup verify-mode tip + column ref | setup | new | shipped upstream (rebase) |
| 119 | C | recommendation layer load needed skills | orchestrator | new | shipped/declined; relates #197/#162 |
| 118 | C | why Ubiquitous Language deprecated | Q | new | usage Q; deprecated skill |
| 117 | C | incomplete ADR after interview | grill-with-docs | new | shipped upstream; relates #299 |
| 115 | C | ctx recommendation engine | orchestrator | new | dup of 183 |
| 112 | C | OpenCode support | platform | new | platform |
| 111 | C | caveman breaks tdd RED→GREEN | caveman/tdd | new | caveman we don't promote |
| 110 | C | I need assistance | — | new | noise |
| 109 | C | grill-me-with-docs ignores ADR & code | grill-with-docs | new | shipped upstream; relates #299/#130 |
| 108 | C | tdd handle missing execute permission | tdd | new | shipped upstream (rebase) |
| 107 | C | #Визуализация | — | new | noise |
| 106 | C | verify/check mode for setup | setup | new | declined upstream (#283 policy) |
| 105 | C | Skillsmith flags TDD false positive | security | new | false positive |
| 104 | C | asking for feedback | — | new | noise |
| 103 | C | marketplace.json /plugin marketplace add | packaging | new | dup of #21/#312 deferred |
| 102 | C | how should grill-me/to-prd/to-issues flow | discussion | new | dup disc themes |
| 101 | C | iteratively build CONTEXT.md brownfield | grill-with-docs | new | shipped upstream; relates #181 |
| 100 | C | Star History README | README | new | cosmetic (dup #135) |
| 99 | C | dex issue tracker backend | triage/to-issues | new | tool we don't use |
| 98 | C | GitLab support issue tracking | setup | new | shipped upstream (rebase) |
| 97 | C | blog links broken | docs | new | shipped upstream (rebase) |
| 96 | C | structured skill metadata validation | packaging | new | shipped upstream (rebase) |
| 95 | C | fractal tree file structures (deep modules) | improve-codebase-architecture | new | relates #180/#303; revisit for fork take |
| 94 | C | f | — | new | noise |
| 93 | C | I think I made a mistake | — | new | noise |
| 89 | C | implement setup + migrate to vague prose | setup | new | shipped upstream (rebase) |
| 88 | C | setup scaffolds repo-specific config | setup | new | shipped upstream (rebase) |
| 87 | C | PRD: Account Data Export (async) | demo PRD | new | generated/demo PRD |
| 79 | C | propagate domain awareness eng skills | domain | new | shipped upstream (rebase) |
| 78 | C | to-issues/to-prd write to local folder | to-issues/to-prd | new | shipped upstream (rebase) |
| 77 | C | SDD in future? | discussion | new | discussion |
| 76 | C | Dust Settled? | — | new | noise |
| 73 | C | no skills found error install | support | new | support |
| 72 | C | install broke after ./skills move | packaging | new | shipped upstream (rebase) |
| 71 | C | HMMMM… | — | new | noise |
| 70 | C | выаыау | — | new | noise |
| 68 | C | new skill for beginners | new skill | new | shipped/declined upstream |
| 63 | C | broader Decision Records beyond ADRs | grill-with-docs | new | shipped upstream; relates #299 |
| 55 | C | why so many stars | — | new | noise |
| 54 | C | NOT WORKING | support | new | support/noise |
| 38 | C | Claude API free trial 求助 | — | new | noise |
| 37 | C | ubiquitous language adds (new)(updated) | ubiquitous-language | new | deprecated skill |
| 33 | C | pop_timeline_green up for review | — | new | spam/noise |
| 31 | C | wrong installation folder | packaging | new | shipped upstream (rebase) |
| 29 | C | ubiquitous language usage | ubiquitous-language | new | deprecated skill |
| 24 | C | tdd add STUB before RED | tdd | new | shipped upstream (rebase) |
| 19 | C | grill-me not always using question tool | grill-me | new | shipped upstream (rebase) |
| 18 | C | grill-me always summarise at end | grill-me | new | shipped upstream; our #240 |
| 17 | C | prd-to-issues don't put tests as slice | to-issues | new | shipped upstream (rebase) |
| 16 | C | grill-me asks 10+ at once | grill-me | new | shipped upstream; our #221/#45 |
| 14 | C | typo setup-pre-commit | setup-pre-commit | new | shipped upstream (rebase) |
| 13 | C | typo setup-pre-commit (dup) | setup-pre-commit | new | dup of 14 |
| 12 | C | grill-me improvement | grill-me | new | shipped upstream (rebase) |
| 11 | C | prefix the skills | packaging | new | shipped upstream (rebase) |
| 10 | C | how to install | Q | new | usage Q |
| 9 | C | recommendation per question grill-me | grill-me | new | shipped upstream (rebase) |
| 6 | C | add MIT license | meta | new | shipped upstream (rebase) |
| 3 | C | native Claude Code marketplace support | packaging | new | dup of #21/#312 deferred |
| 258 | NP | Jira via Rovo MCP issue tracker | triage/to-issues | new | tool we don't use; matches #116 skip |
| 137 | NP | ADR explanation in README | grill-with-docs/README | new | relates #299/disc #302 ADR work; README is a hot rebase file, low priority |
| 135 | NP | GitHub Star History graph in README | README | new | cosmetic; fork doesn't need |
| 92 | NP | execute local issues without sandcastle | platform/infra | new | usage Q, no skill change |
| 91 | NP | marketplace.json for plugin marketplace | packaging | new | dup of #21/#312, already deferred |
| 86 | NP | PRD: Account Data Export | demo PRD | new | generated example, not a skill ask |
| 85 | NP | PRD: RBAC for workspace members | demo PRD | new | generated example |
| 84 | NP | PRD: Notification System | demo PRD | new | generated example |
| 83 | NP | PRD: Notification System (dup) | demo PRD | new | generated example |
| 82 | NP | Feature: RBAC for workspace members | demo PRD | new | generated example |
| 80 | NP | separate content skills from backlog (/github) | orchestrator/packaging | new | architecture idea Matt declined; relates #197/#252 |
| 44 | NP | Codex asked 200 questions | grill | new | question-volume grievance addressed in fork via #221/#240/#45 |
| 20 | NP | health score influenced by match info | unclear | new | noise |
| 15 | NP | "what bullsh*t" | — | new | noise |
