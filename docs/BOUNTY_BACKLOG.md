# Rough enumeration of the bounties we intend to ship, one per phase checkbox.
# Open each as an issue using the .github/ISSUE_TEMPLATE/bounty.yml template,
# then tick the checkbox in docs/ROADMAP.md and link it.
#
# Phase 1
# - policy-registry skeleton + initialize + admin key storage
# - Policy data model (crop / region / threshold / payout schedule)
# - enroll_field + boundary guards
# - fund_policy treasury pool
# - claim_payout from binding index reading
# - withdraw_payout farmer settlement
# - resolve_dispute admin arbitration
# - zero-balance + initialize-once + unauthorized guards
#
# Phase 2
# - oracle-adapter commit_reading (signed, timestamped)
# - finalize_reading exact-rounding breach math
# - challenge_reading dispute window
# - read_current_index / read_latest_payout
# - events for every commit / breach / payout
#
# Phase 3
# - maize / sorghum / cassava / irrigated-rice rainfall tables
# - climate zone classification helper
# - season start / harvest window helper
# - tests against published agro-met reference data
#
# Phase 4
# - cooperative onboarding + policy CRUD screens (dashboard)
# - CSV field enrollment import with bulk validation
# - oracle stream explorer with per-reading drill-down
# - claim audit page (payout -> reading -> formula)
# - Playwright E2E smoke test
#
# Phase 5
# - mobile-first coverage card (farmer app)
# - threshold-neary push alert
# - i18n shell (EN, FR, HA, YO) — each language as its own bounty
#
# Phase 6
# - CHIRPS / open-weather rainfall aggregator adapter
# - index computation worker (deterministic rounding)
# - signed submission script
#
# Cross-cutting
# - GitHub Actions lint + test + wasm build on every PR
# - deploy-testnet.sh
# - docs/API.md endpoints reference
# - SECURITY.md + security policy