# HarvestShield ROADMAP

Milestones map to synthetically-documented issues in the tracker. Work in the
order listed; each milestone is independently mergeable.

## Phase 1 — Policy registry core (contracts)

- [ ] `policy-registry` contract skeleton + `initialize` / admin key storage
- [ ] Policy data model: crop, region, threshold index, payout schedule
- [ ] `enroll_field`: onboard a farmer-lot with a crop calendar
- [ ] `fund_policy`: treasury top-up for the coverage pool
- [ ] `claim_payout`: compute payout from index reading + schedule
- [ ] `withdraw_payout`: farmer claims settled funds
- [ ] `resolve_dispute`: admin arbitration hook for bad readings
- [ ] Boundary guards: initialize-once, not-initialized, unauthorized, zero-balance

## Phase 2 — Oracle adapter (contracts)

- [ ] `oracle-adapter` `commit_reading`: timestamped index value signed by an
      operator key
- [ ] `finalize_reading`: threshold breach computed with exact rounding
- [ ] Dispute window: `challenge_reading` before it becomes binding
- [ ] Pull-model support: `read_current_index`, `read_latest_payout`
- [ ] Event schema for every commit / breach / payout

## Phase 3 — Orchard crop library (contracts)

- [ ] Per-crop rainfall requirement tables (maize, sorghum, cassava, irrigated rice)
- [ ] Climate zone classification helper
- [ ] Season start / harvest window per crop per zone
- [ ] Unit tests against published agro-met reference data

## Phase 4 — Dashboard (apps/dashboard)

- [ ] Cooperative onboarding + policy CRUD screens
- [ ] Field enrollment import (CSV) with bulk validation
- [ ] Oracle stream explorer with per-reading drill-down
- [ ] Claim audit page: payout -> reading -> formula
- [ ] CI + E2E smoke test (Playwright)

## Phase 5 — Farmer app (apps/farmer-app)

- [ ] Mobile-first coverage card (react-hook-form based)
- [ ] Push alerts when an index nears threshold
- [ ] Localization shell (EN, FR, HA, YO) — new-language issues open as bounties

## Phase 6 — Oracles (oracles/)

- [ ] Rainfall aggregator (CHIRPS / open weather API adapters)
- [ ] Index computation worker with deterministic rounding
- [ ] Signed-submission script for the `oracle-adapter`

## Cross-cutting

- [ ] `CONTRIBUTING.md` polished (see repo root)
- [ ] GitHub Actions: lint + test + wasm build on every PR
- [ ] Testnet deploy script (`./scripts/deploy-testnet.sh`)
- [ ] `docs/API.md` for every contract endpoint
- [ ] Security policy + `SECURITY.md`

## How to pick an item

Each checkbox above is (or will become) one or more issues with the full
template: problem & goal, context, implementation details, and verification
requirements. Look for them under the `help-wanted` label, or open one
referencing this file.