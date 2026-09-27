# Tokfare replay

See what your own LLM usage would look like as a per-customer invoice in Korean won (KRW) — in one offline HTML file.

- **What it is**: a single HTML page. Pick a usage file (a generic CSV, or the JSON returned by the OpenAI usage API), enter an exchange rate, its basis date, and a margin, and it builds a per-customer KRW invoice preview from public list prices.
- **Private by design**: the file is read only inside your browser. The page makes **no network requests** (Content-Security-Policy `default-src 'none'`) and does not send or store your data anywhere.
- **Not a bill**: amounts are a preview. Nothing here issues invoices, tax invoices, or charges.
- **Language**: the page UI is in Korean.

## How to use
1. Download `replay.html` from the [latest release](https://github.com/tokfare/replay/releases/latest).
2. Optional: check the file. `shasum -a 256 replay.html` should print the value in `replay.html.sha256` (v0.1.0: `29baae5c6073ec4548f81f5e44d022ba6fe9532706c14ab4b953d29d9cf6a12c`).
3. Open it in a browser (double-click works; no server needed).
4. Enter the exchange rate (KRW per USD), its basis date, and a margin (%). Leave them empty to see USD cost only.
5. Choose a usage file. Try the fake files in [`examples/`](examples/) first.

Supported input:
- **Generic CSV** — header `timestamp,customer,model,input_tokens,output_tokens[,cached_input_tokens]` (any column order). `input_tokens` is the total input including cache hits.
- **OpenAI usage API** — the JSON from `GET /v1/organization/usage/completions` grouped by `project_id` (or `api_key_id`) and `model`.

There is a "hide customer identifiers" switch for screen sharing.

## Method & limits
- Prices: the base per-token input/output prices for chat models of six providers (OpenAI, Anthropic, Google Gemini, Mistral, DeepSeek, xAI; 251 models) from a pinned LiteLLM price file (commit `31678a1`, 2026-09-26). List prices can differ from what you actually pay.
- Not priced in this version: cached input, audio tokens, Batch API, priority processing, and tiered prices. They are listed separately and left out of the totals.
- Models missing from the price table are not guessed; they are listed in a separate "단가 없음" (unpriced) table and left out of the totals.
- VAT (10%) is shown as a separate line. The exchange rate is whatever you enter; the page does not fetch rates.

## Data sources & licenses
- Code in this repository and in `replay.html`: MIT — see [`LICENSE`](LICENSE).
- Price data: LiteLLM `model_prices_and_context_window.json` (MIT, Copyright (c) 2023 Berri AI) — see [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md). The license text is also embedded in the page.
- `examples/` contains fake data only.

## Updates
- Releases are listed in [`CHANGELOG.md`](CHANGELOG.md). Each release attaches `replay.html` and its SHA-256.
- Contact: hello@tokfare.com · Updates: https://tokfare.com/?utm_source=gh-release&utm_medium=tool&utm_campaign=replay-v0.1.0

---

## 한국어

내 LLM 사용량이 고객별 원화 청구서로는 어떻게 보일지, 오프라인 HTML 파일 하나로 확인합니다.

- **무엇인가**: HTML 페이지 하나입니다. 사용량 파일(일반 CSV 또는 OpenAI 사용량 API 응답 JSON)을 고르고 환율·환율 기준일·마진을 넣으면, 공개 원가표로 고객별 원화 청구서 미리보기를 만듭니다.
- **파일은 브라우저 안에서만 읽습니다**: 페이지는 **네트워크 요청을 하지 않고**(CSP `default-src 'none'`), 파일 내용을 어디에도 보내거나 저장하지 않습니다.
- **청구가 아닙니다**: 금액은 미리보기입니다. 청구·세금계산서 발행·결제와 연결되지 않습니다.

### 사용법
1. [최신 릴리스](https://github.com/tokfare/replay/releases/latest)에서 `replay.html`을 내려받습니다.
2. (선택) `shasum -a 256 replay.html` 결과가 `replay.html.sha256`과 같은지 확인합니다.
3. 브라우저로 엽니다(더블클릭, 서버 불필요).
4. 환율(원/USD)·기준일·마진(%)을 넣습니다. 비우면 USD 원가만 보입니다.
5. 사용량 파일을 고릅니다. [`examples/`](examples/)의 가짜 파일로 먼저 해 보세요.

입력 형식: 일반 CSV(헤더 `timestamp,customer,model,input_tokens,output_tokens[,cached_input_tokens]`, `input_tokens`는 캐시 포함 전체 입력), OpenAI `GET /v1/organization/usage/completions` 응답(`project_id` 또는 `api_key_id`와 `model`로 묶음). 화면 공유용 "고객 식별자 가리기" 스위치가 있습니다.

### 방법과 한계
- 원가: 고정한 LiteLLM 가격 파일(커밋 `31678a1`, 2026-09-26)에서 6개 공급사(OpenAI·Anthropic·Google Gemini·Mistral·DeepSeek·xAI) 채팅 모델 251개의 기본 입력·출력 토큰 단가만 씁니다. 공개 단가라 실제 계약 단가와 다를 수 있습니다.
- 이 버전에서 금액에 넣지 않는 것: 캐시 입력, 오디오 토큰, Batch API, 우선 처리, 구간 가격. 따로 보여 주고 합계에서 뺍니다.
- 원가표에 없는 모델은 추정하지 않고 "단가 없음" 표로 따로 보이며 합계에서 뺍니다.
- 부가세(10%)는 별도 줄입니다. 환율은 입력한 값을 쓰며 페이지가 환율을 가져오지 않습니다.

### 출처와 라이선스
- 이 저장소와 `replay.html`의 코드: MIT([`LICENSE`](LICENSE)).
- 원가 데이터: LiteLLM(MIT, Copyright (c) 2023 Berri AI) — [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md). 라이선스 전문은 페이지 안에도 들어 있습니다.
- `examples/`는 가짜 데이터만 있습니다.

### 소식
- 변경 기록은 [`CHANGELOG.md`](CHANGELOG.md)에 있습니다.
- 문의: hello@tokfare.com · 소식 받기: https://tokfare.com/?utm_source=gh-release&utm_medium=tool&utm_campaign=replay-v0.1.0
