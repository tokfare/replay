# Changelog

## v0.2.1 — 2026-09-28
- Release workflow now creates the `pricing-question` label used by the "Pricing question" issue form.
- `replay.html` is unchanged from v0.2.0 (65,238 bytes, SHA-256 `78109cc37b8e45b5d5bf1799b64e2c87f86d0705abeaf986990811b2cf0aea70`).

## v0.2.0 — 2026-09-28
- New pricing modes in `replay.html` (65,238 bytes, SHA-256 `78109cc37b8e45b5d5bf1799b64e2c87f86d0705abeaf986990811b2cf0aea70`):
  - **Credit**: price of 1 credit (KRW, before VAT) and credits per 1,000 input/output tokens, optional per-model rates file → per-customer credits, credit amount, cost, margin, and break-even price of 1 credit; lines where the credit amount is below cost.
  - **Per task**: optional CSV column `task_id` → median, p90 and max cost per task, tasks costing more than an entered price, and a p90-based floor price.
- Credits are the usage-limit unit you define; the tool only calculates and does not sell or hold credits. Taxes and fees are not included.
- New fake examples: `examples/per-task.csv`, `examples/credit-plan.json`.
- Updates links are split by mode (`utm_content=token|credit|per-task`, campaign `replay-v0.2.0`); plain links, followed only when clicked. The page still makes no network requests.
- Release notes now contain only the section for the tag. Issue form "Pricing question" added.
- No change to token-mode pricing or the price snapshot (LiteLLM `31678a1`).

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
