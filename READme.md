# AI Market Research & Strategy Engine

> An end-to-end AI-powered market research platform that automates research planning, web retrieval, evidence extraction, validation, citation generation, and strategy report creation using a multi-agent GenAI workflow.

---

# Project Overview

The **AI Market Research & Strategy Engine** is an Applied GenAI project designed to automate the workflow followed by strategy consulting and market research teams.

Instead of manually searching websites, collecting evidence, validating sources, and preparing reports, this application performs the entire workflow using multiple specialized AI agents.

Users simply enter a research query, and the system generates a structured consulting-style report with validated evidence and citations.

---

# Business Problem

Market research is a time-consuming process involving:

* Searching multiple sources.
* Extracting relevant information.
* Verifying credibility.
* Removing duplicate information.
* Preparing structured reports.

This project automates these steps using an AI pipeline.

### Target Users

* Strategy Consultants
* Business Analysts
* Market Researchers
* Product Managers
* Startup Founders

---

# Product Goal

Build a production-style AI research assistant capable of generating reliable market research reports from a single natural language query while maintaining evidence traceability and source citations.

---

# Key Features

* Multi-Agent AI Workflow
* AI Research Planner
* Web Search using Tavily API
* Evidence Extraction from Web Sources
* Evidence Validation & Credibility Scoring
* Automatic Citation Generation
* McKinsey-style Strategy Report Generation
* Evidence-to-Report Linking
* Supabase Database Integration
* FastAPI Backend
* React Frontend
* Gemini API with Retry & Fallback Logic

---

# System Architecture

User Query
↓
Planner Agent
↓
Research Agent (Tavily Search)
↓
Evidence Extraction Agent
↓
Validation Agent
↓
Citation Builder
↓
Report Agent
↓
Report Linker
↓
Final Strategy Report + Database Storage

### Components

| Layer            | Responsibility             |
| ---------------- | -------------------------- |
| React Frontend   | User Interface             |
| FastAPI Backend  | API & Orchestration        |
| Planner Agent    | Creates research plan      |
| Research Agent   | Collects web sources       |
| Extraction Agent | Extracts evidence          |
| Validation Agent | Validates evidence         |
| Citation Builder | Creates citations          |
| Report Agent     | Generates report           |
| Report Linker    | Links findings to evidence |
| Supabase         | Stores research data       |

---

# AI Workflow

## Stage 1 — Planner Agent

Breaks a research query into structured research tasks.

**Input**

Natural language query.

**Output**

Research tasks with dependencies and objectives.

---

## Stage 2 — Research Agent

Uses Tavily Search API to retrieve relevant web sources for every task.

**Output**

* Source URL
* Title
* Publisher
* Metadata

---

## Stage 3 — Evidence Extraction Agent

Extracts factual claims from retrieved sources using Gemini.

**Output**

* Claim
* Supporting Excerpt
* Entity
* Topic
* Relevance Score

---

## Stage 4 — Validation Agent

Validates extracted evidence using Gemini.

Checks:

* Claim validity.
* Credibility.
* Recency.
* Duplicate detection.
* Conflict detection.

---

## Stage 5 — Citation Builder

Generates citations for validated sources.

---

## Stage 6 — Report Agent

Creates a structured consulting report containing:

* Executive Summary
* Key Findings
* Market Signals
* Competitor Observations
* Strategic Implications
* Recommendations
* Evidence Appendix

---

## Stage 7 — Report Linker

Links every report finding with supporting evidence IDs and citations.

---

# Technology Stack

## Frontend

* React
* Vite
* JavaScript
* CSS

## Backend

* FastAPI
* Python
* Uvicorn
* Pydantic

## AI & APIs

* Google Gemini API
* Tavily Search API

## Database

* Supabase
* PostgreSQL

## Deployment

* Render (Backend)
* Vercel/Render (Frontend)

---

# Project Structure

```text
mckinsey-research-engine/
│
├── frontend/                 # React Frontend
│
├── backend/
│   ├── api/                  # FastAPI Routes
│   ├── services/             # Research Service
│   ├── repositories/         # Supabase Repositories
│   └── main.py               # FastAPI Entry Point
│
├── ai/
│   ├── planner/
│   ├── research/
│   ├── extraction/
│   ├── validation/
│   ├── report/
│   ├── pipeline/
│   ├── browser/
│   ├── llm/
│   └── schemas/
│
├── docs/                     # Architecture & Workflow Docs
├── tests/                    # Unit Tests
├── requirements.txt
└── README.md
```

---

# Database Schema

Supabase tables used:

| Table              | Purpose                  |
| ------------------ | ------------------------ |
| research_jobs      | Stores research requests |
| planner_tasks      | Planner output           |
| sources            | Retrieved web sources    |
| evidence           | Extracted evidence       |
| validation_records | Validation scores        |
| reports            | Generated reports        |
| feedback           | User feedback            |
| memory_records     | Memory foundation        |

---

# API Endpoints

| Endpoint               | Description             |
| ---------------------- | ----------------------- |
| POST /api/research     | Start a research job    |
| GET /api/research      | Fetch all research jobs |
| GET /api/research/{id} | Fetch research result   |
| POST /api/feedback     | Submit report feedback  |

---

# Reliability & Optimizations

The pipeline includes several production-oriented optimizations.

### Retry Logic

* Retries Gemini on temporary failures.
* Exponential backoff.
* Retry sequence: **2s → 4s → 8s**

### Fallback Models

Automatic fallback when the primary Gemini model fails.

### Batch Processing

* Batch Evidence Extraction
* Batch Evidence Validation
* Reduced Gemini API calls.
* Lower token consumption.
* Faster report generation.

### Error Handling

Handles:

* Gemini quota exceeded (429)
* Temporary service unavailable (503)
* Invalid JSON responses
* Missing evidence
* Empty report generation

---

# Evaluation & Testing

### Tested Components

* Planner Agent
* Gemini Connection
* Planner Output Validation
* Dependency Validation
* Research Pipeline
* Evidence Validation

### Pipeline Validation

A successful execution performs:

* Planner creates research tasks.
* Research retrieves web sources.
* Extraction produces evidence.
* Validation scores evidence.
* Citation Builder generates citations.
* Report Agent creates report.
* Report Linker connects findings.

---

# Performance

| Scenario                       | Expected Time  |
| ------------------------------ | -------------- |
| Best Case                      | 45–70 seconds  |
| Average Case                   | 70–120 seconds |
| Worst Case (Retries Triggered) | 2–4 minutes    |

---

# Installation

Clone the repository.

```bash
git clone https://github.com/Priyanshu-Singh1045/mckinsey-research-engine.git
cd mckinsey-research-engine
```

Create virtual environment.

```bash
python -m venv .venv
```

Activate environment.

**Windows**

```powershell
.venv\Scripts\activate
```

Install dependencies.

```bash
pip install -r requirements.txt
```

Run backend.

```bash
uvicorn backend.main:app --reload
```

Run frontend.

```bash
cd frontend
npm install
npm run dev
```

---

# Environment Variables

Create a `.env` file.

```env
GOOGLE_API_KEY=your_gemini_api_key
TAVILY_API_KEY=your_tavily_api_key
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_service_key
```

---

# Sample Research Query

```text
Student placement rate and career outcomes at AlmaBetter compared to other edtech platforms in India.
```

### Output

* Research Tasks
* Web Sources
* Extracted Evidence
* Validation Scores
* Citations
* Executive Summary
* Strategy Recommendations

---

# Screenshots

Add screenshots inside `docs/images/` and reference them here.

### Home Page

`docs/images/homepage.png`

### Pipeline Progress

`docs/images/pipeline.png`

### Generated Report

`docs/images/report.png`

---

# Known Limitations

* Depends on Gemini API availability.
* Free-tier Gemini quota may trigger retries.
* Report quality depends on retrieved web sources.
* Very large research topics increase latency.

---

# Future Improvements

* Vector Memory Retrieval.
* RAG-based Knowledge Store.
* PDF Upload Research.
* Multi-LLM Routing.
* Streaming Report Generation.
* Report Export (PDF & DOCX).

---

# Deployment

| Service  | Status             |
| -------- | ------------------ |
| Backend  | Render             |
| Frontend | Add Deployment URL |
| Database | Supabase           |

---

# Project Highlights

* End-to-end Applied GenAI product.
* Multi-agent AI architecture.
* Automated market research workflow.
* Evidence-grounded report generation.
* Production-style backend and database integration.
* Retry, fallback, batching, and validation for reliability.

---

## Applied GenAI Project Submission

* GitHub Repository
* Live Working Demo
* Demo Video
* Architecture Documentation
* AI Workflow Documentation
* Backend APIs
* Database Integration
* Evaluation & Reliability

---

Built as part of the **Applied Generative AI Project** using **React, FastAPI, Supabase, Tavily Search API, and Google Gemini**.
