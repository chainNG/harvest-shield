# HarvestShield VISION

## One sentence

Smallholder farmers get automatic crop-loss payouts on Stellar, driven by
verifiable weather and yield data, without a claims adjuster in the loop.

## The problem

Crop insurance is actuarially sound but administratively too expensive to
serve smallholders. The cost of inspecting a claim often exceeds the payout,
so insurers either refuse the segment or price everyone out. Meanwhile the
farmer takes 100% of the weather risk with no safety net.

## What we build

A cooperative-owned parametric insurance stack:

1. **Contracts (`contracts/`)** — a `policy-registry` where cooperatives create
   policies, onboard fields, ingest verified index readings, and settle payouts;
   an `oracle-adapter` that commits timestamped off-chain readings on-chain; and
   an `orchard` helper covering crop calendars and rainfall/heat thresholds
   per crop per climate zone.
2. **Dashboard (`apps/dashboard`)** — cooperatives onboard farmers, design payout
   schedules, review oracle streams, and audit settled claims.
3. **Farmer app (`apps/farmer-app`)** — a mobile-first view where a farmer sees
   coverage, live index values for their field, and payout history.
4. **Oracles (`oracles/`)** — feed workers that pull rainfall, temperature, and
   flood-level data, compute the index per the policy, and submit signed
   readings.

## 90% done criteria

- A cooperative can deploy a policy, onboard a farmer, ingest a synthetic
  oracle reading, breach the threshold, and see an automatic payout — end to
  end, on Stellar testnet.
- The `oracle-adapter` supports both push (cooperative submits readings) and
  pull (oracle network writes directly) ingestion.
- Every contract function has unit tests; cross-contract flows have integration
  tests; CI is green on every PR.
- The dashboard can audit any settled claim back to the exact oracle reading
  and payout formula that produced it.

## Non-goals (for now)

- Traditional loss-adjustment claims (visual inspection, photos, drones).
- Underwriting / capital pool management.
- Anything that requires off-chain KYC beyond an admin-listed address.

## Guiding principles

- **Verifiable by default** — every number that drives a payout lives on-chain.
- **Cooperative-owned** — the tool serves the cooperative, not a central issuer.
- **Simple warnings, loud errors** — a policy that cannot settle should refuse
  to exist, not fail silently in the field.