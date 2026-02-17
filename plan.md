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
- [ ] Implement HVM2 Metal CLI + build + runtime + codegen + tests/docs/CI.
- [ ] Pin Bend dependency to Metal-enabled HVM2 revision.
- [ ] Add Bend CLI plumbing (`run-metal` / `gen-metal`).
- [ ] Add Bend compiler target + net-size rules + unsupported-runtime preflight.
- [ ] Update Bend docs.
- [ ] Add Bend CLI tests and snapshots.
- [ ] Run validations and collect results.

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

## Notes
- This file is long-lived and should be updated as milestones complete.
