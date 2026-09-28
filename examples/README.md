# Tokfare replay — example files

All files here are **fake data** made for testing. They contain no real customer, project, or key identifiers.

| File | Format | What it shows |
|---|---|---|
| `generic.csv` | Generic CSV | 3 customers × 4 models, one model missing from the price table, cached input tokens |
| `openai-usage.json` | OpenAI `GET /v1/organization/usage/completions` response | 2 daily buckets, results grouped by `project_id` (one result by `api_key_id`), cached and audio tokens |
| `canary.csv` | Generic CSV | Customer IDs contain a canary string (`REPLAY-CANARY-…`) used to prove the page makes no network requests |
| `per-task.csv` | Generic CSV with `task_id` | 3 customers, 7 tasks (some tasks span several calls) for the per-task pricing check |
| `credit-plan.json` | Per-model credit rates | Made-up credits per 1,000 input/output tokens for 3 models, for the credit pricing check. Not any real company's prices |

## Generic CSV
Header (column order does not matter): `timestamp,customer,model,input_tokens,output_tokens[,cached_input_tokens]`
- `input_tokens` is the **total** input including cache hits. `cached_input_tokens` is the cached part of it.
- Tokens are non-negative integers, up to 1 trillion per row. `timestamp` is `YYYY-MM-DD` or ISO 8601 (no time zone = UTC).

- Optional `task_id`: rows of the same customer with the same `task_id` are one task (per-task check).

## Credit and per-task checks
- **Credit**: enter the price of 1 credit (KRW, before VAT) and default credits per 1,000 input/output tokens. Optionally pick a per-model rates file: `{"models": {"<model>": {"input_per_1k": 0.05, "output_per_1k": 0.2}}}`. The page shows credits used, credit revenue, cost, margin, and the break-even price of 1 credit per customer.
- **Per task**: needs the `task_id` column. The page shows the median, p90 and max cost per task and, if you enter a price per task, how many tasks cost more than that price.
- Both only calculate from the prices you enter. They do not sell or hold credits.

## OpenAI usage response
Save the JSON returned by `GET /v1/organization/usage/completions?group_by=project_id,model` (or `api_key_id`) and open it as is.
- Only the non-cached input and output tokens are priced. Cached, audio, and Batch API usage are listed separately and left out of the totals.

---

# 예시 파일 (한국어)
모든 파일은 테스트용 **가짜 데이터**입니다. 실제 고객·프로젝트·키 식별자는 없습니다.
- `generic.csv`: 일반 CSV. 3고객 × 4모델, 원가표에 없는 모델 1개, 캐시 입력 토큰이 있습니다.
- `openai-usage.json`: OpenAI 사용량 API 응답 형식입니다.
- `canary.csv`: 고객 ID에 카나리 문자열이 들어 있어, 페이지가 네트워크 요청을 하지 않는지 확인하는 데 씁니다.
- `per-task.csv`: `task_id` 열이 있는 일반 CSV. 3고객 7건(여러 호출로 된 건 포함)으로 건당 가격 점검을 봅니다.
- `credit-plan.json`: 모델별 차감률(1,000토큰당 크레딧) 예시. 임의로 만든 값이며 실제 회사 가격이 아닙니다.

크레딧 가격 점검은 1크레딧 가격(원, 부가세 별도)과 기본 차감률을 넣으면 고객별 차감 크레딧·크레딧 매출·원가·마진율·손익분기 1크레딧 가격을 보여 줍니다. 건당 가격 점검은 같은 고객 안에서 `task_id`가 같은 행을 한 건으로 묶어 건당 원가 중앙값·p90·최댓값과, 건당 가격을 넣으면 적자 건 수를 보여 줍니다. 두 점검 모두 입력한 가격으로 계산만 하고 크레딧을 팔거나 보관하지 않습니다.

일반 CSV에서 `input_tokens`는 캐시 적중을 **포함한** 전체 입력이고, `cached_input_tokens`는 그중 캐시분입니다. 캐시·오디오 토큰과 Batch API 사용량은 금액에 넣지 않고 따로 보입니다.
