<!-- plugin-routing:start — synced from the repo owner's cross-repo routing config, which lives outside this repository; the next sync overwrites hand edits to this section, so raise routing changes with the owner -->
## Plugin routing

Before non-trivial work, pick the smallest mix that covers the task: one process skill
first, then the domain skill or agent that does the work. Name the chosen mix in one
line. Skip this for trivial questions and one-line edits. This table only breaks ties
between overlapping installed tools: this repo's AGENTS.md, active task packet and the
rest of this CLAUDE.md take precedence. A packet's `TP_ROUTE … skills=a,b` field names
the skills for that packet and overrides this table.

Where installed skills disagree with each other, these rules decide:
- Questions: brainstorming's questions apply to new work; elsewhere, decide routine calls yourself, state the assumption, and ask only when plausible readings lead to materially different results.
- Tests: while iterating, run the tests that cover the change; run the full suite once before claiming the work is done.
- Commits: commit only when the user or the active task packet authorizes it, even when a skill's flow says to commit.
- Destructive git: never pass `--force` to branch or worktree removal without the user's confirmation, including in `/clean_gone`.
- Other providers: use `codex:rescue` only on the triggers in this table (stuck after two attempts, or an explicit second-opinion request), never proactively.

| intent | triggers | use | not | delegate model → escalate |
|---|---|---|---|---|
| audit | a ROLE line naming an auditor/reviewer/verifier; or keywords: independent audit, audit verdict | independent-audit | verdicts without command output | sonnet → opus (final acceptance) |
| task-packet | a TP_ROUTE key=value line or a TP-… packet id; or keywords: task packet, macropacket | task-packet | — | sonnet → opus |
| pr-ci | a PR URL plus failing CI/checks; or keywords: fix ci, ci failing, failing checks, failing check, red ci | gh-fix-ci | — | sonnet → opus |
| pr-comments | a PR URL plus review comments; or keywords: address comments, address the comments, review comments, review threads | gh-address-comments | — | sonnet → opus |
| pr-merge | merge the pr, merge this pr, ready to merge, merge queue | pr-merge-specialist | merging without the owner's go-ahead | sonnet → opus |
| debug | a traceback or stack trace; or keywords: bug, traceback, exception, crash, crashes, regression, flaky, not working, broken, failing test, failing tests | superpowers:systematic-debugging | guess-and-patch | sonnet → opus |
| review | code review, review the pr, review this pr, review the diff, review my changes, review the change, review the changes | superpowers:requesting-code-review | ad-hoc reread | sonnet → opus (final acceptance) |
| new-work | new feature, build a, add a, let's build, new command, new page, behavior change | superpowers:brainstorming | jumping to code | sonnet → opus |
| implement | implement, tdd, write the code, write tests, unit test, unit tests | superpowers:test-driven-development | — | sonnet → opus |
| finish | ship it, wrap up, wrap it up, finish the branch, open a pr, open the pr, create a pr | superpowers:verification-before-completion | claiming success without output | sonnet → opus |
| skill-authoring | write a skill, new skill, skill.md, edit the skill | superpowers:writing-skills | — | sonnet → opus |
| parallel | in parallel, fan out, independent tasks | superpowers:dispatching-parallel-agents | — | haiku → sonnet |
| isolation | worktree, separate branch, isolate | superpowers:using-git-worktrees | — | haiku → sonnet |
| second-opinion | second opinion, other model, codex rescue | codex:rescue | — | sonnet → opus (final acceptance) |
| ui-build | frontend, landing page, ui component, css, page layout | frontend-design:frontend-design; repo design-system skill first (e.g. adops-design) | — | sonnet → opus |
| ui-review | responsive, accessibility, a11y, design drift, mockup | responsive-accessibility-review; vs a mockup → design-to-code-verification; token drift → design-consistency-review | — | sonnet → opus (final acceptance) |
| copy | headline, cta, tagline, landing copy, marketing copy | copywriting | — | sonnet → opus |
| ux-copy | microcopy, error message, error messages, button label, empty state | ux-writing | — | sonnet → opus |
| charts | chart, plot, data viz, visualization | dataviz | — | sonnet → opus |
| claude-config | hook, hooks, settings.json, permission rule, keybinding, status line, mcp server | update-config; keybindings → keybindings-help; mods → plugin-authoring; "how do I" → claude-code-guide agent | — | haiku → sonnet |
| claude-md | claude.md, project memory | claude-md-management:claude-md-improver | — | sonnet → opus |
| claude-api | anthropic api, claude api, anthropic sdk, prompt caching, model id | claude-api | answering from memory | sonnet → opus |
| code-search | where is, who calls, find usages, trace | Explore agent (broad sweep); serena find_symbol/find_referencing_symbols (exact symbols); dope-context search_code (semantic) | general-purpose for pure search | haiku → sonnet |
| security | security, auth, secret, credential, vulnerability, injection, xss | security-engineer agent | — | opus → operator decision |
| tests | test plan, coverage, edge cases, qa | quality-engineer agent | — | sonnet → opus |
| architecture | architecture, system design, scalability, tradeoff | system-architect agent; Plan agent for an implementation plan | — | opus → operator decision |
| docs | documentation, readme, docstring, guide | technical-writer agent | — | sonnet → opus |
| research | research, compare options, sources, citations | deep-research-agent; gpt-researcher MCP deep_research for a cited report | — | sonnet → opus |
| business | strategy, market, pricing, positioning, business model | business-panel-experts agent | — | opus → operator decision |
<!-- plugin-routing:end -->
