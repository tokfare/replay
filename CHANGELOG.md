# Changelog

## v0.1.1 — 2026-09-27
- `replay.html` now starts with its own license line: `SPDX-License-Identifier: MIT · Copyright (c) 2026 Tokfare` (51,792 bytes, SHA-256 `6065fff5ab75cb595f85f55b3d8aa2dff1a571caf8032cf38e0a616f2f686d11`).
- Updates link campaign: `replay-v0.1.1`.
- Release workflow: `actions/checkout` with `persist-credentials: false`.
- No change to parsing, pricing, or the price snapshot.

## v0.1.0 — 2026-09-27
- First public release of `replay.html` (51,724 bytes, SHA-256 `29baae5c6073ec4548f81f5e44d022ba6fe9532706c14ab4b953d29d9cf6a12c`).
- Inputs: generic CSV and OpenAI usage API (completions) JSON.
- Per-customer KRW invoice preview with exchange rate, basis date, margin, and VAT line; USD-only view when settings are empty.
- Prices: LiteLLM commit `31678a1` (2026-09-26), base chat prices of 251 models from 6 providers.
- No network requests (CSP `default-src 'none'`).
