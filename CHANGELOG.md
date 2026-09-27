# Changelog

## v0.1.0 — 2026-09-27
- First public release of `replay.html` (51,724 bytes, SHA-256 `29baae5c6073ec4548f81f5e44d022ba6fe9532706c14ab4b953d29d9cf6a12c`).
- Inputs: generic CSV and OpenAI usage API (completions) JSON.
- Per-customer KRW invoice preview with exchange rate, basis date, margin, and VAT line; USD-only view when settings are empty.
- Prices: LiteLLM commit `31678a1` (2026-09-26), base chat prices of 251 models from 6 providers.
- No network requests (CSP `default-src 'none'`).
