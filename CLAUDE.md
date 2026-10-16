<!-- plugin-routing:start — generated from ~/.claude/plugin-routing.md by ~/.claude/hooks/sync_plugin_routing.py; edit there, not here -->
## Plugin routing

Before non-trivial work, pick the smallest mix that covers the task: one process skill
first, then the domain skill or agent that does the work. Name the chosen mix in one
line. Skip this for trivial questions and one-line edits. This table only breaks ties
between overlapping installed tools: this repo's AGENTS.md, active task packet and the
rest of this CLAUDE.md take precedence.

| intent | triggers | use | not |
|---|---|---|---|
| debug | bug, error, failing, fails, broken, traceback, exception, crash, regression, flaky, not working | superpowers:systematic-debugging; deep RCA → root-cause-analyst agent; stuck after 2 attempts → codex:rescue | guess-and-patch |
| new work | feature, build a, add a, new command, new page, behavior change, let's build | superpowers:brainstorming → superpowers:writing-plans → superpowers:subagent-driven-development (inline: executing-plans) | jumping to code |
| implement | implement, write the code, tdd, unit test | superpowers:test-driven-development; python code → python-expert agent | — |
| review | review, pull request, PR, diff, audit the change | /code-review (bugs), /simplify (cleanup), /security-review (security); superpowers:requesting-code-review only inside a plan's review loop | ad-hoc reread |
| finish | done, complete, ready to merge, ship it, commit, open a PR | superpowers:verification-before-completion → superpowers:finishing-a-development-branch | claiming success without output |
| second opinion | second opinion, stuck, codex, rescue, other model | codex:rescue (Codex); pal-stdio consensus/challenge for multi-model | — |
| code search | where is, find, locate, who calls, trace, usages | Explore agent (broad sweep); serena find_symbol/find_referencing_symbols (exact symbols); dope-context search_code (semantic) | general-purpose for pure search |
| parallel | in parallel, independent tasks, fan out | superpowers:dispatching-parallel-agents | — |
| isolation | worktree, separate branch, isolate | superpowers:using-git-worktrees | — |
| security | security, auth, secret, credential, vulnerability, injection, xss | security-engineer agent; /security-review for a diff | — |
| tests | test plan, coverage, edge cases, qa | quality-engineer agent | — |
| architecture | architecture, system design, scalability, tradeoff | system-architect agent; Plan agent for an implementation plan | — |
| docs | documentation, readme, docstring, guide | technical-writer agent | — |
| research | research, compare options, latest, sources, citations | deep-research-agent; gpt-researcher MCP deep_research for a cited report | — |
| business | strategy, market, pricing, positioning, business model | business-panel-experts agent | — |
| ui build | ui, frontend, component, landing page, css, layout | repo design-system skill first (e.g. adops-design); else frontend-design:frontend-design; tokens → visual-design-foundations | — |
| ui review | responsive, accessibility, a11y, mockup, screenshot, design drift | responsive-accessibility-review; design-to-code-verification (vs a mockup); design-consistency-review (token drift) | — |
| copy | copy, headline, cta, tagline, microcopy, error message, brand voice | copywriting (marketing pages); ux-writing (in-app text); brand-voice (build a voice profile); brand-content-map (claim sourcing) | — |
| charts | chart, graph, plot, dashboard, visualization | dataviz | — |
| claude config | hook, settings.json, permission, keybinding, plugin, status line, mcp server | update-config; keybindings-help; plugin-authoring; claude-code-guide agent for "how do I" | — |
| claude md | claude.md, agents.md, project memory | claude-md-management:claude-md-improver / revise-claude-md | — |
| claude api | anthropic, claude api, sdk, prompt caching, model id | claude-api | answering from memory |
<!-- plugin-routing:end -->
