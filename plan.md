# Issue #341 - Metal Support Execution Plan

## Issue Context
- Issue: https://github.com/HigherOrderCO/Bend/issues/341
- Request: add non-CUDA GPU support; this implementation targets Metal first.
- Scope: HVM2-first integration; no HVM3/HVM4 migration in this effort.

## Locked Decisions
- Canonical Bend commands: `run-metal`, `gen-metal`.
- Canonical HVM2 commands: `run-metal`, `gen-metal`.
- Target platform for v1: Apple Silicon, macOS 14+.
- Unsupported host/runtime behavior: hard error with actionable guidance.
- Net-size bound for Metal in Bend: 64 nodes.
- Bend consumes temporary HVM2 metal git revision.

## Milestones
- [x] Add long-lived `AGENTS.md`.
- [x] Add long-lived `plan.md`.
- [x] Implement HVM2 Metal CLI + build + runtime + codegen + tests/docs/CI.
- [x] Replace Metal C-runtime shim with native Metal compute evaluator.
- [x] Pin Bend dependency to Metal-enabled HVM2 revision.
- [x] Add Bend CLI plumbing (`run-metal` / `gen-metal`).
- [x] Add Bend compiler target + net-size rules + unsupported-runtime preflight.
- [x] Update Bend docs.
- [x] Add Bend CLI tests and snapshots.
- [x] Run validations and collect results.

## Risks
- Metal backend parity with CUDA may require iterative tuning.
- Upstream HVM2 currently has no Metal runtime; this work adds new platform surface.
- Temporary dependency pin should be replaced by crates.io release when available.
- CI must validate both Linux baseline and macOS Metal path.

## Dependencies
- HVM2 runtime repository: https://github.com/HigherOrderCO/HVM2
- Bend repository: https://github.com/HigherOrderCO/Bend
- Related runtime lines (out of scope for this issue):
  - https://github.com/HigherOrderCO/HVM3
  - https://github.com/HigherOrderCO/HVM4

## Commit Log
- `5fbe8197` chore: add long-lived AGENTS policy
- `aa900700` docs: add metal support execution plan
- `2344f14d` chore(deps): pin hvm to metal-enabled revision
- `c088d8c5` feat(cli): add run-metal and gen-metal commands
- `7670548c` feat(runtime): add metal target behavior and safety checks
- `528f82c0` docs: document metal backend usage and limits
- `ecbe2ee7` test(cli): add metal command coverage
- `5faa716a` chore(deps): bump pinned hvm metal revision
- `66ae404` (HVM2) feat(cli): add run-metal and gen-metal subcommands
- `665ef1f` (HVM2) build: add metal runtime build path
- `ec4757a` (HVM2) feat(runtime): implement metal backend
- `4095877` (HVM2) feat(codegen): add gen-metal standalone output
- `7ff037a` (HVM2) test/docs: add metal validation and docs
- `fd7efe1` (HVM2) fix(codegen): make gen-metal output compileable
- `6a8ca2d` (HVM2) feat(runtime): replace metal shim with native metal evaluator

## Notes
- This file is long-lived and should be updated as milestones complete.
- `cargo test -- --test-threads=1` passes in Bend.
- Bend is now pinned to HVM2 revision `6a8ca2d048d63e461f132afa050f4fad376a83a1` for native Metal compute runtime.
- HVM2 `cargo test --release` currently reports snapshot instability in upstream tests unrelated to this feature work.
