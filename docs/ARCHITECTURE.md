# HarvestShield ARCHITECTURE

## System overview

```
┌──────────────────────────┐
│  Oracle feed workers      │   oracles/ — pull weather/rainfall/flood data,
│  (rainfall, temp, flood)  │   compute the policy index, sign readings
└────────────┬─────────────┘
             │ signed index readings
             ▼
┌──────────────────────────────────────────────┐
│  soroban: oracle-adapter                     │   commits+timestamps reading
│  commit_reading → finalize_reading           │   per policy
└────────────────────┬─────────────────────────┘
             │ binding index value
             ▼
┌──────────────────────────────────────────────┐
│  soroban: policy-registry                    │   thresholds, payout schedule
│  enroll_field / claim_payout / withdraw      │   breach → automatic payout
└────────────┬────────────────┬────────────────┘
             │                │
   ┌─────────▼──────┐  ┌──────▼──────────┐
   │ apps/dashboard  │  │ apps/farmer-app  │
   │ (cooperative)   │  │ (farmer, mobile) │
   └─────────────────┘  └─────────────────┘
```

## Contracts

### policy-registry

Owns the cooperative's insurance book.

| Endpoint | Purpose |
| --- | --- |
| `initialize` | Store admin key, treasury token, app identity |
| `enroll_field` | Register a farmer-lot with crop + region + season |
| `fund_policy` | Top up the coverage pool |
| `claim_payout` | Compute payout from a binding index reading |
| `withdraw_payout` | Farmer claims settled funds |
| `resolve_dispute` | Admin arbitration for challenged readings |

State: policies keyed by `(policy_id, field_id)`; a readable index feed per
policy; per-farmer payout ledger. All money paths guard against empty balance.

### oracle-adapter

Fetches or receives index values and makes them binding.

| Endpoint | Purpose |
| --- | --- |
| `commit_reading` | Signed, timestamped index value for a policy |
| `finalize_reading` | Compute breach against the policy threshold (exact rounding) |
| `challenge_reading` | Start dispute window before a reading binds |
| `read_current_index` | Latest non-binding reading |
| `read_latest_payout` | Latest settled payout for a policy |

### orchard

Pure helper library: crop calendars, per-crop rainfall/heat requirements,
climate-zone classification. No state, no auth — a safe domain for
`good-first-issue` contributions.

## Data flow for a payout

1. Oracle worker fetches rainfall for field's climate zone.
2. Worker computes the season-to-date index for the crop.
3. Worker signs `commit_reading(policy, index, ts)`.
4. `finalize_reading` compares index against the policy threshold.
5. If breached → `claim_payout` computes the payout from the schedule and
   credits the farmer; anyone can invoke, the math is public.
6. Dashboard and farmer app reflect the settlement.

## Web apps

- `apps/dashboard` — Next.js app for cooperatives: policy CRUD, enrollment
  import, oracle stream explorer, claim audit.
- `apps/farmer-app` — mobile-first React app: coverage card, live index,
  payout history, threshold alerts, i18n shell.

Both consume a typed API client (`src/integrations`) contract-first.

## Cross-contract keys

- `PolicyId = (contract_id, u32 nonce)`
- `FieldId = (policy_id, u32 nonce)`
- `IndexReading = (policy_id, u64 timestamp, i128 value, owner)`

## Deficiencies and open questions

- Oracle trust model: single-operator signing today; upgrade path to a
  threshold-of-signers board.
- Treasury vs per-policy pool accounting (v1 keeps one pool per registry).
- Off-chain dispute data (weather station IDs) needs a documented canonical URI
  scheme before dispute resolution can be fully audited.