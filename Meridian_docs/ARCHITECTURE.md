# System Architecture

## Overview

Meridian is a multi-agent AI Market Research & Strategy Engine that automates the complete research workflow from a natural language query to a cited research report.

## Architecture Flow

User Query
    │
    ▼
React Frontend
    │
    ▼
FastAPI Backend
    │
    ▼
Planner Agent
    │
    ▼
Research Agent (Tavily Search)
    │
    ▼
Extraction Agent (Gemini)
    │
    ▼
Validation Agent (Gemini)
    │
    ▼
Citation Builder
    │
    ▼
Report Agent (Gemini)
    │
    ▼
Report Linker
    │
    ▼
Supabase Database + Frontend Report UI

## Components

### Frontend
- React + Vite + Tailwind CSS
- Supabase Authentication
- Dashboard, Research History, Report Viewer

### Backend
- FastAPI REST API
- Repository pattern
- Supabase PostgreSQL persistence

### AI Pipeline
- Planner Agent
- Research Agent
- Extraction Agent
- Validation Agent
- Citation Builder
- Report Agent
- Report Linker

### External Services
- Google Gemini API
- Tavily Search API
- Supabase
