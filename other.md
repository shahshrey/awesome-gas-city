# Other Gas City projects

The [README](README.md) lists packs and tools built to be reused. This page lists the rest of a GitHub survey run on October 15, 2026: personal cities, products that embed a pack for their own repository, and packs that should not be imported as-is.

Few of these are worth importing. Several contain one idea worth borrowing.

**[`^        back to top        ^`](#)**

## Ideas worth borrowing

- [saymyname-app/agent-factory](https://github.com/saymyname-app/agent-factory) - Watchdog orders: session-loop guard, mayor context guard, model staleness, backup freshness, orphan sweep, idle-work wake. `No license file`
- [Davidcode2/bright-lights-gascity-config](https://github.com/Davidcode2/bright-lights-gascity-config) - Housekeeping orders on top of gastown: spawn-storm detect, orphan sweep, gate sweep, prune branches, wisp compact. `No license file`
- [KyleBarton/securegascity](https://github.com/KyleBarton/securegascity) - Runs every agent inside a [nono](https://nono.sh) kernel sandbox (Landlock on Linux, Seatbelt on macOS). `No license file`
- [lmist/humalike2](https://github.com/lmist/humalike2) - One formula per bead type (`bug`, `chore`, `spike`, `decision`, `story`, and others), with polecats in isolated worktrees. `No license file`
- [rpmessner/we_go_next_dev](https://github.com/rpmessner/we_go_next_dev) - A `proposer` fed by a `propose-features` order and a `triager` fed by `triage-backlog`, so the factory fills its own queue. `No license file`
- [brettinternet/pr-watch](https://github.com/brettinternet/pr-watch) - One long-lived agent per open pull request, keeping CI green and working through review. `No license file`
- [Matt2021-A/matt-city](https://github.com/Matt2021-A/matt-city) - A non-coding city: researcher, skeptic, writer, and voice editor, with a separate identity per principal. `No license file`
- [blueflyio/gluless](https://github.com/blueflyio/gluless) - Formula v2 `check.exec` proves a written goal was met, instead of trusting an agent's "done". ([Source Code](https://github.com/blueflyio/gluless)) `Apache-2.0`
- [mmlac/gascity-pack-mmlac](https://github.com/mmlac/gascity-pack-mmlac) - Polecats split by model (Haiku, Sonnet, Opus) with Codex reviewers as fallback. Wired through the old rig `includes` mechanism; read it, don't import it. `No license file`
- [mfhens/opendebt](https://github.com/mfhens/opendebt) - An event-driven intake order that watches for new petitions and pours a scaffold formula. Schema 1. `NOASSERTION`

## Workshop and demo packs

All three are from Actual AI, which runs the Software Factory Intensive.

- [actual-software/sf-tutorial](https://github.com/actual-software/sf-tutorial) - The workshop library: `base-factory`, bead and PR gates, multi-vendor reviewers, and a self-improvement loop. `No license file`
- [actual-software/software-factory-intensive](https://github.com/actual-software/software-factory-intensive) - Lesson packs (planner, architect, designer, builder, reviewer, validator, release gate) and tracker sync orders. `No license file`
- [actual-software/actual-factory-demo](https://github.com/actual-software/actual-factory-demo) - A 15-minute, five-agent factory from an ASCII-art task to an open pull request. `No license file`

## Factories built for one product

- [deepkawal/software-factory](https://github.com/deepkawal/software-factory) - Enterprise reference architecture for regulated delivery: intake PM, product and architecture reviewers, and a release gate. Mostly documentation. `MIT`
- [sverka-dev/sverka](https://github.com/sverka-dev/sverka) - A local-first check runner whose own repository is built by a Gas City factory, including stacked-PR formulas. `MIT`
- [shapeandshare/anvil](https://github.com/shapeandshare/anvil) - Feature, refactor, and investigation formulas, plus `anvil-human-decision` so waiting on a person is an explicit step. `MIT`
- [abapify/adt-cli](https://github.com/abapify/adt-cli) - A TypeScript toolkit for SAP ABAP. Its `gascity/` pack drives the project's own work. `MIT`
- [Dauliac/gasville](https://github.com/Dauliac/gasville) - One `code-workflow` formula (spec, refine, implement in waves, review, persist) and an `on-epic-close` order. `No license file`
- [Borghese-Gladiator/new-tech-monorepo](https://github.com/Borghese-Gladiator/new-tech-monorepo) - Mostly copies of gastown formulas. The orders `review-before-merge` and `verify-on-change` are the interesting part. `No license file`
- [EarthSciML/EarthSciAST](https://github.com/EarthSciML/EarthSciAST) - One chore formula, `mol-update-spec-schema`, inside a research codebase. `AGPL-3.0`
- [justintanner/apicity](https://github.com/justintanner/apicity) - One formula, `mol-apicity-release`, for release automation. `MIT`
- [nicholasspencer/butane_flutter](https://github.com/nicholasspencer/butane_flutter) - A rig overlay that adds Dart and Flutter review rubrics on top of a generic pack. `No license file`
- [idvorkin/idvorkin.github.io](https://github.com/idvorkin/idvorkin.github.io) - The working config behind Igor Dvorkin's write-ups: a `blogsmith` agent and journal formulas. `No license file`
- [repldriven/factory](https://github.com/repldriven/factory) - City in a `gascity/` subdirectory, with orders to snapshot agent branches and stamp a merge strategy. `No license file`

## Tools that ship a pack as glue

- [trillium/parlay](https://github.com/trillium/parlay) - A chat channel per background agent, including voice from a phone. The pack is deployment glue. `MIT`
- [jsgerman-oss/gascity-cockpit](https://github.com/jsgerman-oss/gascity-cockpit) - A VS Code extension that drives several cities through the Gas City `/v0` API. `MIT`
- [gastownhall/acp-unreal](https://github.com/gastownhall/acp-unreal) - An Agent Client Protocol adapter so `gc` can drive Unreal Agent sessions. A provider, not a workflow. `MIT`
- [craigcode/kranz](https://github.com/craigcode/kranz) - A separate mission-control harness (fresh worker per feature, independent validators, a human approval record) that also runs inside a city. `MIT`
- [thinkjones/intelligent-package-manager](https://github.com/thinkjones/intelligent-package-manager) - A Claude Code plugin builder. Its `pack.toml` is test data for assembling kits. `MIT`
- [ThePlenkov/gascity-devcontainer](https://github.com/ThePlenkov/gascity-devcontainer) - Devcontainer features for Gas City, Devin, and Claude. Schema 1, with pinned `bd` and `core` imports. `No license file`
- [outdoorsea/switchyard-packs](https://github.com/outdoorsea/switchyard-packs) - Archived mirror. The README says `switchyard-ops` and `switchyard-build` are retired. `No license file`

## Domain towns

From [The Academic Wasteland](https://github.com/academic-wasteland/research-commons), a federated research project at BioHackathon 2026. These show cities talking to each other.

- [academic-wasteland/research-commons](https://github.com/academic-wasteland/research-commons) - An `rcp-pack` that validates research tasks and maps them onto beads. `Apache-2.0`
- [academic-wasteland/pangenome-town](https://github.com/academic-wasteland/pangenome-town) - Peer questions answered with deterministic `vg` and `bcftools` queries, via an `answer-peer` formula and an `inbox-dispatch` order. `No license file`
- [anuragxxd/nalanda](https://github.com/anuragxxd/nalanda) - A GA4GH WES workflow broker. A single `broker` agent admits and translates requests and executes nothing itself. `Apache-2.0`

## Minimal personal cities

One or two agents, usually a mayor. Useful only as layout examples.

- [kabeero/dotfiles](https://github.com/kabeero/dotfiles) - A mayor and a coder in a dotfiles repository. `GPL-3.0`
- [erks/bootstrap](https://github.com/erks/bootstrap) - A mayor inside a Mac setup repository. `No license file`
- [rosejas13/Portfolio](https://github.com/rosejas13/Portfolio) - A mayor inside a Next.js portfolio site. `GPL-3.0`

## Rejected

- [donnabox/gc-import](https://github.com/donnabox/gc-import) - A URL-based pack manager. Schema 1, superseded by built-in `gc import`. `No license file`
- [donnabox/gc-packman](https://github.com/donnabox/gc-packman) - A tap-based pack manager on the old workspace `includes` model. `No license file`
- [joe-mcgovern/gc-pack-planners](https://github.com/joe-mcgovern/gc-pack-planners) - Named planner pools. Schema 1, April 2026. The idea is reusable; the config is not. `No license file`
- [joe-mcgovern/gc-pack-reviewers](https://github.com/joe-mcgovern/gc-pack-reviewers) - A multi-phase review pipeline (correctness, tests, modularity, elegance, security, polish). Schema 1. `No license file`
- [stevebargelt/gascity-packs](https://github.com/stevebargelt/gascity-packs) - A stale schema 1 snapshot of official packs, with no README. `No license file`
- [ShawnSpooner/pack-city-pipeline](https://github.com/ShawnSpooner/pack-city-pipeline) - Targets Gas Town (`gt pack add`), not Gas City. `No license file`
- [mfhens/osm2](https://github.com/mfhens/osm2) - Schema 1 intake orders, and no README. `NOASSERTION`
- [julianknutsen/rc-smoke-pack](https://github.com/julianknutsen/rc-smoke-pack) - A one-agent fixture used to test `gc pack registry publish` for v1.4.0-rc1. `No license file`
- [RemanenetSpy/beads-memory-smriti](https://github.com/RemanenetSpy/beads-memory-smriti) - "Temporal memory" via a third-party hosted MCP service. No tests, no license, and the registry entry its README claims was not in the public catalogue. `No license file`

## False positives

These matched a `pack.toml` search and are not Gas City packs.

- [EonsofStupid/Clyffy_Avatar](https://github.com/EonsofStupid/Clyffy_Avatar) - A 3D avatar asset pack.
- [SeanOC/stuff](https://github.com/SeanOC/stuff) - 3D-printable designs. No `pack.toml` on the default branch at survey time. `MIT`
