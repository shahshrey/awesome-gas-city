# Awesome Gas City

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of packs, tools, guides, and talks for [Gas City](https://github.com/gastownhall/gascity), the open-source orchestration-builder SDK for multi-agent software factories.

Gas City takes the machinery from Steve Yegge's [Gas Town](https://github.com/gastownhall/gastown) and turns it into configurable building blocks, so a team can define its own agent shape instead of accepting a fixed one. Julian Knutsen and Chris Sells built it; Yegge is lightly affiliated and did not write it. A factory here is configuration you own: agents (who), formulas (how), and orders (when), packaged as packs and pointed at repositories (rigs). Every unit of work is a durable bead.

Surveyed October 15, 2026, against Gas City **v1.5.0** (October 5, 2026). This page keeps packs and tools built for reuse. Factories and tools shaped around one product are on the [Other](other.md) page.

See [Contributing](#contributing).

--------------------

## Contents

- [Platform](#platform)
- [Documentation](#documentation)
- [Tutorials and workshops](#tutorials-and-workshops)
- [Packs](#packs)
  - [Build methodologies](#build-methodologies)
  - [Roles and baselines](#roles-and-baselines)
  - [Pull requests and review](#pull-requests-and-review)
  - [Memory and knowledge](#memory-and-knowledge)
  - [Chat, intake, and runtimes](#chat-intake-and-runtimes)
  - [Cost and operations](#cost-and-operations)
  - [Examples and teaching packs](#examples-and-teaching-packs)
  - [Domain packs](#domain-packs)
- [Guides and write-ups](#guides-and-write-ups)
- [Video and podcasts](#video-and-podcasts)
- [Community](#community)
- [Related](#related)
- [Practices](#practices)
- [External links](#external-links)

--------------------

## Platform

**[`^        back to top        ^`](#)**

- [Gas City](https://github.com/gastownhall/gascity) - The SDK. Zero hardcoded roles: every role arrives through a pack. ([Releases](https://github.com/gastownhall/gascity/releases), [Dashboard](https://factory.gascity.com/city/maintainer-city/)) `MIT` `Go`
- [gascity-packs](https://github.com/gastownhall/gascity-packs) - The official opt-in packs. Import with `gc import add` so `packs.lock` pins the commit. The repository has no root `LICENSE` file; the Slack packs are MIT.
- [Pack registry](https://registry.gascity.com/) - The public catalogue. The published list is the 16 official `gastownhall` packs; community packs below were found by search, not the registry. ([Catalogue](https://github.com/gascity/registry/blob/main/public/registry.toml))
- [Gas Town Hall](https://github.com/gastownhall) - The GitHub organization for Gas City, Gas Town, and Beads.

The six primitives, from [How Gas City Works](https://github.com/gastownhall/gascity/blob/main/docs/getting-started/how-gas-city-works.md):

| Primitive | Role | What it is |
| --- | --- | --- |
| Agent | Who | A configured worker. While it runs, it is a session. |
| Bead | What | One unit of work. Tasks, mail, sessions, and convoys differ by type. |
| Formula | How | A reusable method. Compiling it materializes a bead graph that outlives the file. |
| Rig | Where | An external project, usually a git repository, registered with the city. |
| Pack | Configures | A directory with `pack.toml`: agents, formulas, and orders. The city is the root pack. |
| Event | Observe | An append-only notification (`bead.closed`, `session.crashed`, `order.fired`). |

An order pairs a trigger (cooldown, cron, condition, event, or manual) with a formula or a shell script. `gc sling` creates a bead and routes it in one step.

Import a pack from its upstream repository:

```toml
[imports.gc]
source = "https://github.com/gastownhall/gascity-packs.git//gascity"

[imports.toolkit]
source = "https://github.com/zookanalytics/gc-toolkit"
```

Then run `gc import install`. A path with `.git//` selects a subdirectory. Local paths take no version pin.

--------------------

## Documentation

**[`^        back to top        ^`](#)**

- [docs.gascity.com](https://docs.gascity.com/tutorials) - Tutorials 01–07: cities and rigs, agents, sessions, communication, formulas, beads, orders. ([Quickstart](https://docs.gascity.com/getting-started/quickstart), [Harness recipes](https://docs.gascity.com/guides/harness-recipes), [Shareable packs](https://docs.gascity.com/guides/shareable-packs))
- [docs.gascityhall.com](https://docs.gascityhall.com/) - The Mintlify documentation site.
- [Guide index](https://gascity.com/guide/) - Product guides: [Build an AI Software Factory](https://gascity.com/guide/ai-software-factory/), [Reference architecture](https://gascity.com/guide/software-factory-reference-architecture/), [A factory in practice](https://gascity.com/guide/software-factory-examples/), [Beads with Jira, Linear, and GitHub Issues](https://gascity.com/guide/beads-with-jira-linear-github-issues/).
- [The City Wire](https://blog.gascity.com/) - Release posts that double as feature tutorials: [1.3](https://blog.gascity.com/posts/gas-city-1-3-now-were-looping-with-gas/), [1.4](https://blog.gascity.com/posts/gas-city-1-4-the-view-from-the-factory-floor/), [Beads 1.3 and Gas City 1.5](https://blog.gascity.com/posts/beads-1-3-and-gas-city-1-5/).
- [How Gas City Works](https://github.com/gastownhall/gascity/blob/main/docs/getting-started/how-gas-city-works.md) - The six primitives and the orchestrator, bead store, and event bus.
- [Installation](https://github.com/gastownhall/gascity/blob/main/docs/getting-started/installation.md) - Homebrew installs `gc` plus tmux, jq, git, Dolt, flock, and Beads. `brew install gascity`.
- [Coming from Gas Town](https://github.com/gastownhall/gascity/blob/main/docs/getting-started/coming-from-gastown.md) - How mayor, polecat, crew, refinery, witness, deacon, and dog map onto configuration.
- [Understanding Formulas](https://github.com/gastownhall/gascity/blob/main/docs/guides/understanding-formulas.md) - Formula v2, checks, retries, and why a formula without the v2 opt-in collapses into one bead.
- [Formula spec v2](https://github.com/gastownhall/gascity/blob/main/docs/reference/specs/formula-spec-v2.md) - The specification.
- [Understanding Packs](https://github.com/gastownhall/gascity/blob/main/docs/guides/understanding-packs.md) - Imports, patches, and agent defaults. Patch an imported agent instead of forking the pack.
- [Configuring an Agent](https://github.com/gastownhall/gascity/blob/main/docs/guides/configuring-an-agent.md) - The five axes: harness, model, upstream, transport, and runtime.
- [Multi-agent engineering environment](https://github.com/gastownhall/gascity/blob/main/docs/guides/multi-agent-engineering-environment.md) - The three layers: portable pack, city deployment, machine-local `.gc/`.
- [Command execution trust boundaries](https://github.com/gastownhall/gascity/blob/main/docs/reference/trust-boundaries.md) - Operator-configured commands are a feature, not a sandbox.
- [Troubleshooting](https://github.com/gastownhall/gascity/blob/main/docs/getting-started/troubleshooting.md) - Dolt mode, endpoint drift, and backups. ([Runbooks](https://github.com/gastownhall/gascity/tree/main/docs/troubleshooting), [docs.gascity.com](https://docs.gascity.com/getting-started/troubleshooting))
- [FAQ](https://github.com/gastownhall/gascity/blob/main/docs/getting-started/faq.md) - Built-in harnesses, including Claude Code, Codex, Gemini CLI, Cursor Agent, GitHub Copilot, Amp, OpenCode, Grok, Kimi Code, and Pi.
- [deps.env](https://github.com/gastownhall/gascity/blob/main/deps.env) - The pinned toolchain CI actually runs.

--------------------

## Tutorials and workshops

**[`^        back to top        ^`](#)**

- [actual-software/sf-tutorial](https://github.com/actual-software/sf-tutorial) - The Software Factory Intensive curriculum: labs W1–W7 and L1–L5, hardening labs, and the `base-factory` everyone starts from. `No license file`
- [actual-software/software-factory-intensive](https://github.com/actual-software/software-factory-intensive) - The hands-on workshop repository. `No license file`
- [Software Factory Intensive](https://www.actual.ai/softwarefactory) - Actual AI's workshop schedule, run with the Gas City maintainers. ([New York, May 11 2026](https://actual.ai/softwarefactory/new-york-may-11-2026), [Seattle, August 18](https://actual.ai/softwarefactory/seattle-aug-18))
- [Standing Up Gas City](https://idvork.in/gas-city-home) - Igor Dvorkin. The scaffolder is the spec: run `gc init`, then customize. The most useful first-week write-up.
- [The City Wrote This](https://idvork.in/gas-city-rig) - Igor Dvorkin. Building `gc` from HEAD, and what the first rig cost.
- [Turning the Dark Factory Lights On](https://www.davesgroundtruth.com/turning-the-dark-factory-lights-on/) - David Koleczek (April 18, 2026). An early walkthrough of cities, rigs, and how Gas Town relates to Gas City.
- [Tom Rochette's notes](https://tomrochette.com/agents/orchestration/gascity/) - Install notes current to 1.5, including Homebrew and Beads 1.3.1.
- [Etienne Segal's notes](https://www.esegal.me/tooling/Gas-City---gascity-SDK) - A short tooling note.
- [langlabs: gastownhall/gascity](https://langlabs.io/gastownhall/gascity) - Install, API, examples, and gotchas.
- [Gas City: Multi Agent Orchestration SDK im Check 2026](https://nevercodealone.de/de/vibe-coding/vibe-coding-modelle/gascity-orchestration-sdk-multi-agent-vibe-coding-2026) - A German overview.
- [gc-dispatch on Tessl](https://tessl.io/registry/skills/github/crypt0nerd1/gascity/gc-dispatch/evals) - A community skill that routes work with `gc sling` and formulas.
- [r/ClaudeAI: Gas City tutorial using Claude Code](https://www.reddit.com/r/ClaudeAI/comments/1t8crn4/gas_city_tutorial_using_claude_code/) - A community setup thread.

--------------------

## Packs

**[`^        back to top        ^`](#)**

Packs below are the 27 repositories from that survey that are built to be reused. Descriptions note when a pack is niche, older than about July 2026, or has no `LICENSE` file. Check the license before vendoring one into company code.

Formula v2 adoption is uneven. Without `[requires] formula_compiler = ">=2.0.0"`, a formula runs as v1: one bead, one agent, no `check` or `retry`. The strongest v2 examples here are mathcity, upstream-city, and gc-toolkit. The official packs themselves are mostly still v1.

### Build methodologies

**[`^        back to top        ^`](#)**

Official build packs share launch variables (`interaction_mode`, `review_mode`, `drain_policy`, `push`, `open_pr`), so switching methodology is a change of formula name. Import one at city scope and sling it, for example `--on bmad-build`. Rig-scoped worker roles come from `gascity/roles`.

- [gascity](https://github.com/gastownhall/gascity-packs/tree/main/gascity) - The default starter. `build-basic` walks requirements, plan, plan review, decomposition, parallel implementation, a three-lane review, and finalize. `No license file`
- [bmad](https://github.com/gastownhall/gascity-packs/tree/main/bmad) - BMAD as a factory: PRD, architecture, epics and stories, a readiness gate, story-by-story implementation, then adversarial review. `No license file`
- [compound-engineering](https://github.com/gastownhall/gascity-packs/tree/main/compound-engineering) - The widest reviewer fanout: correctness, security, performance, migrations, and API contracts each get a lane. `No license file`
- [superpowers](https://github.com/gastownhall/gascity-packs/tree/main/superpowers) - Jesse Vincent's Superpowers process: design approval, written-spec approval, per-task test-driven development, then spec-compliance and code-quality review. `No license file`
- [gstack](https://github.com/gastownhall/gascity-packs/tree/main/gstack) - garrytan/gstack mapped onto Gas City: office-hours intake, plan review, staff review, QA, security, and release readiness. `No license file`
- [gc-toolkit](https://github.com/zookanalytics/gc-toolkit) - A complete roster that replaces gastown rather than layering on it: work, review, planning, and maintenance, with 11 of 18 formulas on v2. Tests and CI. `MIT`
- [sdlc-discipline-pack](https://github.com/reggieperry/sdlc-discipline-pack) - A six-pool chain (planner, worker, tester, reviewer, documenter, finalizer) with no named sessions. Hand off with `gc.routed_to`, never `--assignee`, or pools stall. Aimed at Python and pytest. Formulas are v1; last pushed July 9, 2026. `MIT`
- [omg](https://github.com/atilla777/omg) - "Oh My Gas City." Requirements to an approved spec, then a Beads breakdown, then development, with explicit human approvals. `MIT`
- [upstream-city](https://github.com/bbrowning/upstream-city) - A city config, and a strong model of N=2 independent review, strict synthesis, and an at-most-three revise loop. Twelve v2 formulas. `MIT`
- [cacc-twin-team](https://github.com/wespd/cacc-twin-team) - A Claude mayor over Codex workers for the standard gascity roles. `No license file`
- [bluewater](https://github.com/boylec/bluewater) - A naval chain of command: 83 agents, 32 formulas, and cross-provider two-key launches for risky operations. Last pushed April 27, 2026, v1 formulas only. Mine it for ideas. `MIT`

### Roles and baselines

**[`^        back to top        ^`](#)**

- [agentops](https://github.com/boshu2/agentops) - A thin role pack (`agentops-executor`, `agentops-factory`) over Gas City 1.4 routing, inside the AgentOps project. `Apache-2.0`
- [gastown](https://github.com/gastownhall/gascity-packs/tree/main/gastown) - The Gas Town shape as a pack: coordinator roles, rig workers, patrol formulas, and a dog pool for stuck-agent shutdown warrants. `No license file`
- [gascity-custom-packs](https://github.com/Dawnvael/gascity-custom-packs) - A personal collection of 22 agents and 13 formulas. Fourteen deprecated `graph.v2` keys. `No license file`
- [oversight-rig](https://github.com/gastownhall/gascity-packs/tree/main/oversight-rig) - One rig-scoped project lead per rig, so the mayor stops triaging every project. Optional Obsidian-compatible portfolio brief. `No license file`
- [riley-gc-packs](https://github.com/rileywhite/riley-gc-packs) - `basic`: one import composing `bd`, `core`, `gascity`, worker roles, and a mayor. Commits are pinned. Models are chosen by capability tier (frontier, deep, standard, light), not by name. `MIT`

### Pull requests and review

**[`^        back to top        ^`](#)**

- [contributing-to-gascity](https://github.com/gastownhall/gascity-packs/tree/main/contributing-to-gascity) - The external-contributor lifecycle for `gastownhall/gascity`, with the project's review standards baked into the skill text. Self-contained. `No license file`
- [gascity-explore](https://github.com/bmt/gascity-explore) - Agents may branch and push, and cannot land on main without a human merge. `MIT`
- [gastown-beads-lite-pack](https://github.com/philcunliffe/gastown-beads-lite-pack) - Gastown on SQLite `beads-lite` instead of Dolt. Some deprecated `graph.v2` keys. May 2026. `No license file`
- [pr-pipeline](https://github.com/gastownhall/gascity-packs/tree/main/pr-pipeline) - Author-side formulas: plan an issue, map blast radius, self-review against an 11-category scorecard, and run a pre-push gate. None of them push or open a pull request. `No license file`
- [pr-pipeline-beads-lite-pack](https://github.com/philcunliffe/pr-pipeline-beads-lite-pack) - The same pipeline on `beads-lite`. `No license file`
- [pr-review](https://github.com/gastownhall/gascity-packs/tree/main/pr-review) - Adopt a contributor pull request with a Claude, Codex, and Gemini review, a human gate, then a publish handoff to the mayor. `No license file`
- [pr-review-beads-lite-pack](https://github.com/philcunliffe/pr-review-beads-lite-pack) - The multi-model adopt-PR formulas on `beads-lite`. `No license file`

### Memory and knowledge

**[`^        back to top        ^`](#)**

- [bartertown-pack](https://github.com/Wldc4rd/bartertown-pack) - A knowledge forum in git, over MCP, where mayors trade fixes across cities. No server. `MIT`
- [cass](https://github.com/gastownhall/gascity-packs/tree/main/cass) - Search past coding-agent sessions with [cass](https://github.com/Dicklesworthstone/coding_agent_session_search). A shared prompt fragment works across Claude, Codex, and Gemini. `No license file`
- [ddd-pack](https://github.com/dstengle-gascity/ddd-pack) - Domain-Driven Design templates (PDR, ADR, runbook, platform standard, ubiquitous language) and a mechanical linter that enforces them. April 2026. `No license file`
- [GasCityHistoryMan](https://github.com/dlarsen5/GasCityHistoryMan) - Advisory knowledge in SQLite: `gc historyman brief`, `record-fact`, `record-handoff`, `reflect`. It refuses to store workflow state, so Beads stays the source of truth. CI. `MIT`
- [hindsight-gc-pack](https://github.com/Toady00/hindsight-gc-pack) - A shared memory bank over PRDs, specs, and ADRs. A city-scoped archivist is the only writer (`max_active_sessions = 1`), with nightly consolidation. Needs a Hindsight server. `No license file`

### Chat, intake, and runtimes

**[`^        back to top        ^`](#)**

- [discord](https://github.com/gastownhall/gascity-packs/tree/main/discord) - A workspace-hosted Discord provider: bot token, interactions, and admin services under `.gc/services/discord/`. Do not load it beside the older `discord-intake` pack. `No license file`
- [gc-mattermost-pack](https://github.com/Wldc4rd/gc-mattermost-pack) - Real-time agent-to-agent and agent-to-human chat over self-hosted Mattermost. `MIT`
- [github](https://github.com/gastownhall/gascity-packs/tree/main/github) - GitHub App intake: signed webhooks, durable receipts, and addressed messages such as `@mayor`. `No license file`
- [runtime-cloudflare](https://github.com/gastownhall/gascity-packs/tree/main/runtime-cloudflare) - A runtime executable that speaks the Runtime Provider Protocol and proxies sessions to a Cloudflare Worker. Ships on its own cadence, with no Go dependency on `gc`. `No license file`
- [slack-channel](https://github.com/gastownhall/gascity-packs/tree/main/slack-channel) - A few named sessions share channels with distinct identities. No slash commands. `MIT`
- [slack-full](https://github.com/gastownhall/gascity-packs/tree/main/slack-full) - Slash commands, modals, peer fanout, launcher-mode spawning, and multi-rig channel routing. `MIT`
- [slack-mini](https://github.com/gastownhall/gascity-packs/tree/main/slack-mini) - The mayor posts status into a single channel. No bindings, no state. `MIT`
- [tavily-gascity-pack](https://github.com/Tavily-FDE/tavily-gascity-pack) - Registers Tavily's remote MCP server (search, extract, crawl, map, research) for every agent. Adds no agents and runs no local server. Maintained by the vendor. `No license file`

### Cost and operations

**[`^        back to top        ^`](#)**

- [gascity-packs (patrol-toolchain)](https://github.com/pot-ai-to/gascity-packs) - Keeps deacon, witness, and boot suspended until silence or staleness wakes them. A direct lever on the patrol-token burn in [gascity #458](https://github.com/gastownhall/gascity/issues/458). May 2026. `MIT`
- [profiler](https://github.com/gastownhall/gascity-packs/tree/main/profiler) - Profiles a finished formula run from the workflow root bead, against sources that are already durable. No launch-time opt-in. `No license file`

### Examples and teaching packs

**[`^        back to top        ^`](#)**

- [coder-critic](https://github.com/gascity/coder-critic) - A frozen two-coder workflow on a Beads dependency graph, with recorded run evidence. `MIT`
- [gascity-cookbook](https://github.com/thinkjones/gascity-cookbook) - Recipes, a provider-tier pack (`fast-worker`, `solid-worker`, `deep-thinker` mapped per city), and two copy-me cities. `MIT`
- [tinker-city](https://github.com/wierdbytes/tinker-city) - A Tokyo Night Storm tmux theme and a Claude usage widget. A clean example of `session_live` hooks. macOS only. `No license file`

### Domain packs

**[`^        back to top        ^`](#)**

- [funsearch-pack](https://github.com/jjgarzella/funsearch-pack) - FunSearch-style evolutionary program search with agent mutators. `Apache-2.0`
- [julia-tools-pack](https://github.com/jjgarzella/julia-tools-pack) - Formulas that take a Julia package to registration quality. `No license file`
- [mathcity](https://github.com/tdupu/mathcity) - Twelve sub-packs for mathematics research: agents file evidence, gates check readability, a human adjudicates. Thirty-one v2 formulas and a large test suite. The brief-and-gate pattern carries to other domains. `GPL-3.0`

--------------------

## Guides and write-ups

**[`^        back to top        ^`](#)**

### From the people who built it

- [Welcome to Gas City](https://steve-yegge.medium.com/welcome-to-gas-city-57f564bb3607) - Steve Yegge (April 24, 2026). The launch essay. Also on [yegge.ai](https://yegge.ai/essays/welcome-to-gas-city/).
- [Welcome to Gas Town](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04) - Steve Yegge. The predecessor, and where the vocabulary comes from.
- [Welcome to the Wasteland](https://steve-yegge.medium.com/welcome-to-the-wasteland-a-thousand-gas-towns-a5eb9bc8dc1f) - Steve Yegge. A public commons of many towns.
- [Announcing Gas City 1.0](https://sellsbrothers.com/announcing-gas-city-1-0) - Chris Sells (April 28, 2026). What a software factory is, and the prompt shape his agents use.
- [Orchestration Is All You Need](https://sellsbrothers.com/orchestration-is-all-you-need) - Chris Sells (April 21, 2026). Coding CLIs as factory workers, and multi-vendor review.

### From people who ran one

- [two days at the first software factory intensive](https://avi.mn/blog/software-factory-intensive) - Akhilesh Rangani (April 27, 2026). Determinism comes from the graph of steps, not from a smarter prompt. Fix the config, not the chat.
- [Inside the 100-agent Software Factory](https://every.to/context-window/inside-the-100-agent-software-factory) - Every (May 19, 2026). A measured review. Verdict there: learn from the ideas, skip the toolkit for now.
- [Gas City: inside the software factory with 100 coding agents](https://theautomationgroup.nl/en/blog/gas-city-software-factory-100-agents-en) - The Automation Group. Worth a look if you already run more than about ten Claude Code sessions and are willing to read source.
- [Gas City: Orchestration, Not a Smarter Prompt](https://idvork.in/gas-city) - Igor Dvorkin. Orchestration earns its keep when the work is plural and carries judgment.
- [Building Production Grade Applications using Agent Orchestration](https://foursignals.dev/blog/2026-07-31-agent-orchestration-adventures-to-build-a-production-grade-application) - Gene Conroy-Jones (July 31, 2026). Eight weeks, three deployed services. Most of the time went into the factory.
- [AI Agent Development Workflow from Brief to Pull Request](https://foursignals.dev/blog/2026-08-27-ai-agent-development-workflow-from-brief-to-pull-request/) - Gene Conroy-Jones (August 27, 2026). Gates, cold plan review, and a kaizen loop after every epic.
- [Gas City](https://rywalker.com/research/gas-city) - Ry Walker. A research profile: audit trail and runtime flexibility, against a heavy dependency stack and unbounded cost.
- [Gas City vs CoSim](https://tannerjc.net/blog/gas-city-vs-cosim/) - James Tanner (May 8, 2026). Estimates $500–2,000 per month, and treats the two as complementary.
- [A Day in Gas Town](https://www.dolthub.com/blog/2026-01-15-a-day-in-gas-town/) - DoltHub (January 15, 2026). Beads on Dolt, before Gas City shipped.
- [Trying Out Gas Town](https://gabewyatt.com/blog) - Gabe Wyatt (March 8, 2026). Gas Town failure shapes (orphaned Dolt processes, patrols killing infrastructure, false "done") that Gas City still inherits.

### Comparisons published by Gas City

- [Gas City vs Factory.ai](https://gascity.com/guide/gas-city-vs-factory-ai/)
- [Gas City vs 8090](https://gascity.com/guide/gas-city-vs-8090-software-factory/)
- [Software factories vs agent frameworks](https://gascity.com/guide/software-factories-vs-agent-frameworks/)

### Discussions

- [Hacker News: Welcome to Gas City](https://news.ycombinator.com/item?id=48015146) - Mostly sceptical: what problem this solves, whether adversarial review is proven, and whether the jargon earns its keep.
- [Hacker News: Gas Town, from clown show to v1.0](https://news.ycombinator.com/item?id=47770124) - More mixed. The bottleneck moves from coding speed to specs and validation.
- [Tim Abell: Anyone tried Gas City?](https://www.linkedin.com/posts/timabell_anyone-tried-gas-city-or-gas-town-or-activity-7462920953262538771-Va_A) - LinkedIn (May 20, 2026).
- [r/ClaudeAI: Is there actually a good way to orchestrate…](https://www.reddit.com/r/ClaudeAI/comments/1ua3252/is_there_actually_a_good_way_to_orchestrate)
- [r/claudexplorers: Orchestrators less bloated than Gas Town](https://www.reddit.com/r/claudexplorers/comments/1qstyn0/orchestrators_that_are_less_bloated_than_gas_town/)

Operational evidence lives in the issue tracker. Start with [Witness agent cost analysis (#458)](https://github.com/gastownhall/gascity/issues/458), [Reconciler drain-log loop (#855)](https://github.com/gastownhall/gascity/issues/855), and [Supervisor restarts on transient Dolt EOF (#663)](https://github.com/gastownhall/gascity/issues/663).

--------------------

## Video and podcasts

**[`^        back to top        ^`](#)**

Gas City was about six months old at survey time. Most "Gas" videos are about Gas Town. Searching YouTube for "Gas City" mostly returns Gas City, Indiana.

If you watch only a few:

1. [Moving to Gas County, parts 2–5](https://www.youtube.com/playlist?list=PLKC0meZlaqcTtb7Qpz86exniYUJ-OlIrv) - Rainydan. Live walkthroughs of the official tutorials.
2. [My Gas City Setup: Adversarial Agents, TDD, and a Custom tmux Dashboard](https://www.youtube.com/watch?v=bYPkQisCag8) - Kenny Loveall (May 31, 2026, 24 min). The most concise real configuration tour.
3. [Building a Software Factory with Gas City](https://www.youtube.com/watch?v=9rGJQ02puc0) - Agents and Engineers, with Stephanie Jarmak (October 4, 2026, 79 min). ([Episode page](https://agentsandengineers.com/episodes/0018-building-a-software-factory-with-gas-city/))
4. [First impressions of Steve Yegge's Gas City](https://www.youtube.com/watch?v=yoHHVgddUyI) - Enterprise Vibe Code #44 (April 20, 2026, 1h54m).
5. [The Future of Software Development: Embracing AI and Quality](https://www.youtube.com/watch?v=FWh9TCSFdZw) - Chris Sells with Very Good Ventures (July 22, 2026, 61 min). ([Write-up](https://verygood.ventures/blog/chris-sells-gas-city-future-of-software-development-ai-and-quality/))

### Live coding

- [Moving to Gas County](https://www.youtube.com/playlist?list=PLKC0meZlaqcTtb7Qpz86exniYUJ-OlIrv) - Rainydan, 63 parts (May–July 2026), streamed on [Twitch](https://www.twitch.tv/rainydan) and archived to YouTube. Parts 1–6 follow the official tutorials: [intros](https://www.youtube.com/watch?v=9f2Oa2klKrM), [cities, rigs, agents, sessions](https://www.youtube.com/watch?v=Fe-UFzHjqyg), [communication and formulas](https://www.youtube.com/watch?v=5IgV6qTApwA), [beads and orders](https://www.youtube.com/watch?v=HEVnzVFf7m0), [nine contributor concepts](https://www.youtube.com/watch?v=XQ9UiPAsrFA), [session architecture](https://www.youtube.com/watch?v=gCFe5T2qyqQ). Parts 27–36 are the most useful stretch for pack, Dolt, and worktree questions.
- [Welcome to Gas City and Can I find a Job](https://www.youtube.com/watch?v=dlsTB-HPv5g) - Joey Perrello (April 25, 2026, 2h13m). A livestream the day after launch. Partly off-topic.

### Interviews

- [How Software Factories Use Agent Context](https://www.youtube.com/watch?v=7bH7fxN4P5A) - Chris Sells with Yugabyte (September 25, 2026).
- [Gas Town Refinery #1](https://www.youtube.com/watch?v=nY1h_UY_T34) - Chris Sells and Steve Yegge (February 18, 2026, 1h23m). The [official channel](https://www.youtube.com/@gastownhall-yt)'s only upload at survey time. Pre-1.0, and the origin story.
- [From Vibe Code to Fleet Mode](https://www.youtube.com/watch?v=i_iMweHXvDY) - Steve Yegge at IT Revolution (June 1, 2026, 22 min). ([Also on IT Revolution](https://videos.itrevolution.com/watch/1184927954/))
- [Inside Steve Yegge's Software Factory](https://www.youtube.com/watch?v=I3iRsti-Lmw) - re:cinq (September 20, 2026, 69 min). Mostly the Gas Town factory for Wyvern, with Gas City mentioned.
- [Steve Yegge's call to action for the Wasteland](https://www.youtube.com/watch?v=cFEvz5vUQ7M) - John Tigue (~February 2026, 8 min). Beads, then Gas Town, then Gas City, then the Wasteland.
- [Software Engineering Daily: Gas Town, Beads, and Agentic Development](https://softwareengineeringdaily.com/podcasts/gas-town-beads-and-the-rise-of-agentic-development-with-steve-yegge/) - Steve Yegge.

Live "Gas City Demo & Q/A" webinars with Knutsen and Sells have no public recordings. Schedule: [July 1](https://actual.ai/softwarefactory/online-july-1), [September on Luma](https://luma.com/sfi-webinar-september).

### Related Gas Town videos

Useful for beads, the mayor, polecats, the refinery, and convoys.

- [The AI Vampire with Gas Town's Steve Yegge](https://www.youtube.com/watch?v=9UDLl9Q0azA) - Scott Hanselman (March 3, 2026, 36 min).
- [You'll Never Write Code the Same Way Again](https://www.youtube.com/watch?v=Rgwu9nF_Xok) - Steve Yegge on Tessl (July 6, 2026, 57 min).
- [Agentic Security: Permissions, Provenance, and the Agent Supply Chain](https://www.youtube.com/watch?v=yWS0udrIOc8) - Steve Yegge at AI Engineer (July 20, 2026, 22 min).
- [Gastown, Claude, and the Rise of AI Factories](https://www.youtube.com/watch?v=l7PB_ovm8A4) - TWiT Intelligent Machines (February 12, 2026, 36 min).
- [I Let 30 AI Agents Loose in My Repo](https://www.youtube.com/watch?v=_mrMidIwCzk) - Better Stack (7 min).
- [Orchestrating Multi-Agent Development at Scale with Gas Town](https://www.youtube.com/watch?v=OE20MCpQ1KQ) and [Revisited 3 Months Later](https://www.youtube.com/watch?v=vl0fEHeNc4o) - Ryan MacLean.

--------------------

## Community

**[`^        back to top        ^`](#)**

- [Discord](https://discord.gg/xHpUGUzZp2) - Gas Town Hall. About 2,600 members at the 1.0 announcement.
- [@gastownhall](https://x.com/gastownhall) - Release announcements.
- [@csells](https://x.com/csells) - Chris Sells.
- [Steve Yegge on the launch](https://x.com/Steve_Yegge/status/2047582408799584394) - The post pointing at the essay.
- [Maintainer City](https://factory.gascity.com/city/maintainer-city/) - A read-only public view of the factory that maintains the project's own repositories.

--------------------

## Related

**[`^        back to top        ^`](#)**

- [Beads](https://github.com/gastownhall/beads) - The durable work graph (`bd`). It is what an agent reads when it wakes with no memory of yesterday. `MIT` `Go`
- [Dolt](https://github.com/dolthub/dolt) - The git-versioned SQL database under Beads. Every state change is a write and a commit. `Apache-2.0`
- [Gas Town](https://github.com/gastownhall/gastown) - The fixed-shape predecessor. Still maintained, and shipped inside Gas City as the `gastown` pack.
- [MEOW](https://steve-yegge.medium.com/welcome-to-gas-city-57f564bb3607) - Molecular Expression of Work. A formula is poured into a molecule of beads. Described in the Gas City launch essay.

People comparing toolkits usually land on one of these, which are not Gas City packs:

| Alternative | When people reach for it | Where that claim is made |
| --- | --- | --- |
| Gas Town | You want the opinionated topology and the larger community. | [rywalker.com](https://rywalker.com/research/gas-city) |
| A coding agent and its subagents | The work is one session, or light delegation. | [Hacker News](https://news.ycombinator.com/item?id=48015146), [tannerjc.net](https://tannerjc.net/blog/gas-city-vs-cosim/) |
| A thin layer on Linear or Jira | The team already lives in that tracker. | [The Automation Group](https://theautomationgroup.nl/en/blog/gas-city-software-factory-100-agents-en) |
| Factory.ai, 8090 | A commercial software factory. | [gascity.com comparisons](https://gascity.com/guide/) |

--------------------

## Practices

**[`^        back to top        ^`](#)**

Drawn from the maintainers, the Actual AI workshop, and people who ran a factory on real work. The long form of each one is in the linked source.

1. **Start from a working factory.** Import `gascity` `build-basic`, or the workshop's `base-factory`. Change one layer at a time. ([A factory in practice](https://gascity.com/guide/software-factory-examples/), [sf-tutorial](https://github.com/actual-software/sf-tutorial))
2. **Let `gc init` write the config.** Hand-writing `pack.toml` from the docs is how first attempts go subtly wrong. ([Standing Up Gas City](https://idvork.in/gas-city-home))
3. **Put control flow in formulas, not prompts.** The graph is fixed when the formula is compiled. Declare `[requires] formula_compiler = ">=2.0.0"` on every new formula. Cook with `gc formula cook` before you sling. ([avi.mn](https://avi.mn/blog/software-factory-intensive), [Understanding Formulas](https://github.com/gastownhall/gascity/blob/main/docs/guides/understanding-formulas.md))
4. **Fix the prompt file, not the chat.** A chat correction is a tax you pay again. A committed template is a tax you pay once. ([avi.mn](https://avi.mn/blog/software-factory-intensive))
5. **Pair a doer with a checker.** Review across vendors when you can: three models catch different bugs than one model three times. Give reviewers a document to cite. ([Welcome to Gas City](https://steve-yegge.medium.com/welcome-to-gas-city-57f564bb3607), [Announcing Gas City 1.0](https://sellsbrothers.com/announcing-gas-city-1-0))
6. **Gate the front of the queue.** A vague bead produces a guessed implementation. A gate has to block, record a reason, and be tested on a case that fails. ([sf-tutorial](https://github.com/actual-software/sf-tutorial))
7. **"Done" should mean a script agrees.** `[steps.check]`, exec orders, and doctor checks cost nothing per run. A witness that answers "all clear" most of the time is a shell script wearing a model bill. In one gastown-pack deployment, witness patrols were about 69% of API spend. ([#458](https://github.com/gastownhall/gascity/issues/458))
8. **Match the tool to the decision.** Orchestration pays when the work has many steps and real judgment. For one deterministic task, a city is overhead. Drop the mayor for one-shot work. ([Gas City: Orchestration, Not a Smarter Prompt](https://idvork.in/gas-city))
9. **Pin packs and read the diff before upgrading.** `gc import status`, then `gc reload`. Share packs, not city directories: `.gc/` is machine-local. ([sf-tutorial W7](https://github.com/actual-software/sf-tutorial))
10. **Budget for rough edges.** A room of experienced engineers took a full day to get running at the New York workshop. Pin `gc`, `bd`, and Dolt. Keep the city small until you trust it. ([Every](https://every.to/context-window/inside-the-100-agent-software-factory), [deps.env](https://github.com/gastownhall/gascity/blob/main/deps.env))

Anti-patterns, in short: correcting agents in chat, control flow inside prompts, advisory gates, unpinned imports, LLM patrols for yes-or-no checks, and a mayor in front of one-shot work.

--------------------

## External links

**[`^        back to top        ^`](#)**

- [O'Reilly Radar: Trends to Watch, June 2026](https://oreillyradar.substack.com/p/radar-trends-to-watch-june-2026)
- [Nate's Newsletter: AI Agent Judge Layer](https://natesnewsletter.substack.com/p/agent-judge-layer-production-control)
- [MLOps Community: MCP Servers Behaving Badly](https://mlopscommunity.substack.com/p/mcp-servers-behaving-badly)
- [Downstream, August 8, 2026](https://buttondown.com/downstreamnews/archive/downstream-saturday-august-8-2026/)
- [jakub-m bulletin 2026-05-01](https://github.com/jakub-m/bulletin/blob/mainline/bulletins/bulletin-2026-05-01.md)

--------------------

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

This list is licensed under [CC BY-SA 4.0](LICENSE). Projects it links to keep their own licenses.
