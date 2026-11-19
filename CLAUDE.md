<!-- plugin-routing:start — synced from the repo owner's cross-repo routing config, which lives outside this repository; the next sync overwrites hand edits to this section, so raise routing changes with the owner -->
## Plugin routing

Before non-trivial work, pick the smallest mix that covers the task: one process skill
first, then the domain skill or agent that does the work. Name the chosen mix in one
line. Skip this for trivial questions and one-line edits. This table only breaks ties
between overlapping installed tools: this repo's AGENTS.md, active task packet and the
rest of this CLAUDE.md take precedence. A packet's `TP_ROUTE … skills=a,b` field names
the skills for that packet and overrides this table.

Model IDs are pinned in the routing tiers. A tier does not grant calls, retries,
paid fallback, provider substitution, audit independence or final acceptance.
Verify the actual runner/account, input scope and finite grant before dispatch.
Fable (claude-fable-5-1) is exceptional and requires explicit native authority;
Fleet Fable invocations through Claude Code require invocation-scoped
ANTHROPIC_BASE_URL=http://127.0.0.1:47821, never a global proxy change.

Where installed skills disagree with each other, these rules decide:
- Questions: brainstorming's questions apply to new work; elsewhere, decide routine calls yourself, state the assumption, and ask only when plausible readings lead to materially different results.
- Tests: while iterating, run the tests that cover the change; run the full suite once before claiming the work is done.
- Commits: commit only when the user or the active task packet authorizes it, even when a skill's flow says to commit.
- Destructive git: never pass `--force` to branch or worktree removal without the user's confirmation, including in `/clean_gone`.
- Other providers: use `codex:rescue` only on the triggers in this table (stuck after two attempts, or an explicit second-opinion request), never proactively.

| intent | triggers | use | not | delegate model → escalate |
|---|---|---|---|---|
| audit | a ROLE line naming an auditor/reviewer/verifier; or keywords: run an independent audit, perform an independent audit, do an independent audit, need an independent audit, independently audit, you are the independent auditor | independent-audit | verdicts without command output | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| task-packet | a TP_ROUTE key=value line or a TP-… packet id; or keywords: task packet, macropacket | task-packet | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| pr-ci | a PR URL plus failing CI/checks; or keywords: fix ci, ci failing, failing checks, failing check, red ci | gh-fix-ci | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| pr-comments | a PR URL plus review comments; or keywords: address comments, address the comments, review comments, review threads | gh-address-comments | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| pr-merge | merge the pr, merge this pr, ready to merge, merge queue | pr-merge-specialist | merging without the owner's go-ahead | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| debug | a traceback or stack trace; or keywords: bug, traceback, exception, crash, crashes, regression, flaky, not working, broken, failing test, failing tests | superpowers:systematic-debugging | guess-and-patch | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| review | code review, review the pr, review this pr, review the diff, review my changes, review the change, review the changes | superpowers:requesting-code-review | ad-hoc reread | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| new-work | new feature, build a, add a, let's build, new command, new page, behavior change | superpowers:brainstorming | jumping to code | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| implement | implement, tdd, write the code, write tests, unit test, unit tests | superpowers:test-driven-development | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| finish | ship it, wrap up, wrap it up, finish the branch, open a pr, open the pr, create a pr | superpowers:verification-before-completion | claiming success without output | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| skill-authoring | write a skill, new skill, skill.md, edit the skill | superpowers:writing-skills | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| parallel | in parallel, fan out, independent tasks | superpowers:dispatching-parallel-agents | — | claude-haiku-5-5 medium → claude-sonnet-5-5 medium |
| isolation | create a worktree, new worktree, use a worktree, in a worktree, in a new worktree, git worktree add, separate branch, new branch | superpowers:using-git-worktrees | — | claude-haiku-5-5 medium → claude-sonnet-5-5 medium |
| second-opinion | second opinion, other model, codex rescue | codex:rescue | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| ui-build | frontend, landing page, ui component, css, page layout | frontend-design:frontend-design; repo design-system skill first (e.g. adops-design) | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| ui-review | responsive, accessibility, a11y, design drift, mockup | responsive-accessibility-review; vs a mockup → design-to-code-verification; token drift → design-consistency-review | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| copy | headline, cta, tagline, landing copy, marketing copy | copywriting | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| ux-copy | microcopy, error message, error messages, button label, empty state | ux-writing | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| charts | chart, plot, data viz, visualization | dataviz | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| claude-config | settings.json, settings.local.json, permission rule, permission rules, keybinding, keybindings, add an mcp server, add mcp server, update-config | update-config; keybindings → keybindings-help; mods → plugin-authoring; "how do I" → claude-code-guide agent | — | claude-haiku-5-5 medium → claude-sonnet-5-5 medium |
| claude-md | update claude.md, update the claude.md, edit claude.md, edit the claude.md, improve claude.md, improve the claude.md, audit claude.md, audit the claude.md, revise claude.md, revise the claude.md, fix claude.md, claude.md improver, claude.md quality | claude-md-management:claude-md-improver | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| claude-api | anthropic api, claude api, anthropic sdk, prompt caching, model id | claude-api | answering from memory | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| code-search | where is, who calls, find usages, trace | Explore agent (broad sweep); for exact symbols or semantic search use serena find_symbol/find_referencing_symbols or dope-context search_code if those MCP servers are connected, otherwise Grep/Glob | general-purpose for pure search | claude-haiku-5-5 medium → claude-sonnet-5-5 medium |
| security | security, auth, secret, credential, vulnerability, injection, xss | security-engineer agent | — | claude-opus-5-5 high → operator decision |
| tests | test plan, coverage, edge cases, qa | quality-engineer agent | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| architecture | architecture, system design, scalability, tradeoff | system-architect agent; Plan agent for an implementation plan | — | claude-opus-5-5 high → operator decision |
| docs | documentation, readme, docstring, guide | technical-writer agent | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| research | research, compare options, sources, citations | deep-research-agent; for a cited report use gpt-researcher MCP deep_research if that server is connected, otherwise deep-research-agent with WebSearch/WebFetch | — | claude-sonnet-5-5 medium → claude-opus-5-5 high |
| business | strategy, market, pricing, positioning, business model | business-panel-experts agent | — | claude-opus-5-5 high → operator decision |
<!-- plugin-routing:end -->
