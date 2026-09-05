# API Documentation

## Authentication

All protected endpoints require:

Authorization: Bearer <supabase_access_token>

---

## POST /api/research/

Starts a new research pipeline.

### Request

{
  "query": "Impact of Generative AI on education."
}

### Response

Returns a research job and generated report after pipeline execution.

---

## GET /api/research/

Returns authenticated user's research history.

---

## GET /api/research/{job_id}

Returns a specific research report.

---

## GET /docs

FastAPI Swagger UI.

---

## Backend Services

- PlannerTaskRepository
- SourceRepository
- EvidenceRepository
- ValidationRepository
- ReportRepository
