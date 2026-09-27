# Tokfare replay — example files

All files here are **fake data** made for testing. They contain no real customer, project, or key identifiers.

| File | Format | What it shows |
|---|---|---|
| `generic.csv` | Generic CSV | 3 customers × 4 models, one model missing from the price table, cached input tokens |
| `openai-usage.json` | OpenAI `GET /v1/organization/usage/completions` response | 2 daily buckets, results grouped by `project_id` (one result by `api_key_id`), cached and audio tokens |
| `canary.csv` | Generic CSV | Customer IDs contain a canary string (`REPLAY-CANARY-…`) used to prove the page makes no network requests |

## Generic CSV
Header (column order does not matter): `timestamp,customer,model,input_tokens,output_tokens[,cached_input_tokens]`
- `input_tokens` is the **total** input including cache hits. `cached_input_tokens` is the cached part of it.
- Tokens are non-negative integers, up to 1 trillion per row. `timestamp` is `YYYY-MM-DD` or ISO 8601 (no time zone = UTC).

## OpenAI usage response
Save the JSON returned by `GET /v1/organization/usage/completions?group_by=project_id,model` (or `api_key_id`) and open it as is.
- Only the non-cached input and output tokens are priced. Cached, audio, and Batch API usage are listed separately and left out of the totals.

---

# 예시 파일 (한국어)
모든 파일은 테스트용 **가짜 데이터**입니다. 실제 고객·프로젝트·키 식별자는 없습니다.
- `generic.csv`: 일반 CSV. 3고객 × 4모델, 원가표에 없는 모델 1개, 캐시 입력 토큰이 있습니다.
- `openai-usage.json`: OpenAI 사용량 API 응답 형식입니다.
- `canary.csv`: 고객 ID에 카나리 문자열이 들어 있어, 페이지가 네트워크 요청을 하지 않는지 확인하는 데 씁니다.

일반 CSV에서 `input_tokens`는 캐시 적중을 **포함한** 전체 입력이고, `cached_input_tokens`는 그중 캐시분입니다. 캐시·오디오 토큰과 Batch API 사용량은 금액에 넣지 않고 따로 보입니다.
