# Evaluation & Reliability

## Successful Test Cases

- Planner Agent generates research tasks.
- Research Agent retrieves web sources.
- Extraction Agent extracts evidence.
- Validation Agent validates evidence.
- Citation Builder generates citations.
- Report Agent generates structured reports.

## Reliability Features

### Retry Logic
- Retry attempts: 3 per Gemini model.
- Exponential backoff: 2s → 4s → 8s.

### Fallback Strategy
1. Gemini 3.5 Flash
2. Gemini 3.5 Flash Lite
3. Gemini 3.6 Flash (recommended future fallback)

### Optimizations
- Batch extraction (5 sources/request).
- Batch validation (20 evidence/request).
- Report generation uses top 15 evidence items.

## Failure Handling

- HTTP 429 → retry after delay.
- HTTP 503 → exponential backoff.
- Invalid JSON → cleaned before parsing.
- Empty response → graceful failure.

## Performance

| Stage | Expected Time |
|-------|---------------|
| Planner | 2–5 sec |
| Research | 5–12 sec |
| Extraction | 10–25 sec |
| Validation | 4–10 sec |
| Report | 4–8 sec |
| Best Case Total | 25–40 sec |
| Worst Case Total | 2–4 minutes |
