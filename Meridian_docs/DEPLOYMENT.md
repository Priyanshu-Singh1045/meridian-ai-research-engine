# Deployment Guide

## Frontend

Platform: Vercel

Environment Variables:
- VITE_SUPABASE_URL
- VITE_SUPABASE_ANON_KEY
- VITE_API_BASE_URL

Build Command:
npm run build

Output Directory:
dist

## Backend

Platform: Render

Start Command:
uvicorn backend.main:app --host 0.0.0.0 --port $PORT

Environment Variables:
- GOOGLE_API_KEY
- TAVILY_API_KEY
- SUPABASE_URL
- SUPABASE_KEY

## Database

Supabase PostgreSQL with authentication enabled.

## Live Services

- Backend: Render
- Database: Supabase
- AI Models: Gemini
- Search Engine: Tavily
