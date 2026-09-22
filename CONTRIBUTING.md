# Contributing to HarvestShield

Thanks for your interest. HarvestShield is explicitly built to be worked on by
many contributors, so this guide makes it easy to pick up an issue and ship it.

## Finding work

- `good-first-issue` — small, well-bounded, with the acceptance criteria spelled out.
- `help-wanted` — larger; still fully specified.
- Outside issues, [`docs/ROADMAP.md`](docs/ROADMAP.md) lists every planned milestone
  with the issues that track it.

Every issue follows a strict template, so you always know:
1. the **problem & goal**,
2. the **context & components** involved,
3. the exact **implementation details**, and
4. the **verification & testing requirements** that define *done*.

## Setup

```bash
# contracts
cargo build --release --target wasm32-unknown-unknown -p policy-registry
cargo test --workspace

# dashboard / farmer app
pnpm install
pnpm --filter dashboard dev
```

## Workflow

1. Comment on the issue you want, and ask for assignment.
2. Create a branch: `git checkout -b <owner>/<issue-slug>`.
3. Implement, matching the existing style (see lints below). Do not add
   code comments the code does not need.
4. Add or update tests. Fill any Soroban snapshot files the test run produces.
5. Run the full suite and the linter locally.
6. Open a PR against `main`, reference the issue (`Closes #NN`), and note how
   you verified the acceptance criteria.

## Checks

```bash
cargo fmt --all -- --check
cargo clippy --workspace -- -D warnings
cargo test --workspace
```

## Review expectations

- PRs are small and single-purpose.
- Every PR that changes contract behaviour adds or updates tests.
- No secrets, keys, or real mainnet funds in tests.
- Public API names follow the existing conventions (snake_case endpoints,
  `Error` variants in the contract's enum).

## Code of conduct

Be respectful. Disagreement about code is normal; personal attacks are not.
HarvestShield is a global project and every contributor deserves a safe space.