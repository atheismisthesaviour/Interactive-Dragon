# BrandGuard AI Backend

AI-assisted brand governance API for pre-publication content review.

## Status
MVP foundation. Built for the event build window; disclose AI services and validate all findings with a human reviewer.

## Run locally

```bash
python -m venv .venv
# Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Open `/docs` for the interactive API docs and `/health` for the health check.

## Core capabilities
- Brand workspaces, guidelines, approved facts, terminology and assets
- Text review with evidence-linked findings and suggested fixes
- Image checks for dimensions, format, dominant colours and approved-logo similarity
- Human review decisions, comments and revision history
- Analytics for recurring issue categories
- Optional LLM review via `OPENAI_API_KEY`; deterministic checks remain available without it

## Privacy and safety
- Do not upload confidential customer material to external AI providers unless the organisation has approved that provider.
- AI findings are advisory; only authorised humans can approve content.
- Set a strong `APP_SECRET_KEY` and configure `CORS_ORIGINS` before production use.
- The default SQLite database is for demo/local use. Configure managed PostgreSQL for production.

## Environment
Copy `.env.example` to `.env` and configure values. Never commit secrets.

## Event disclosure
This project uses FastAPI, SQLAlchemy, Pillow, and optional OpenAI API integration. The team must accurately disclose AI assistance, libraries, APIs and each member's contribution. Follow the event's official build-window rules.
