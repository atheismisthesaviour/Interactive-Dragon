# BrandGuard AI — API quick start

Base URL: `http://localhost:8000` locally; Render URL after deployment.
Interactive API documentation: `/docs`.

## 1. Create a brand workspace
`POST /api/brands`
```json
{"name":"Acme Demo","description":"Sample brand for judging","primary_color":"#1f4b99"}
```

## 2. Add approved sources
`POST /api/brands/{brand_id}/guidelines`
```json
{"title":"No unsupported superlatives","rule":"Avoid: world's leading","category":"claims","severity":"high"}
```
`POST /api/brands/{brand_id}/facts`
```json
{"statement":"Founded in 2018","source":"https://example.org/about"}
```
`POST /api/brands/{brand_id}/terminology`
```json
{"term":"customers","preferred":"clients","note":"Use approved audience terminology"}
```

## 3. Review text
`POST /api/brands/{brand_id}/review/text`
```json
{"title":"Launch post","creator":"Demo Creator","content":"We are the world's leading platform for customers."}
```
Response includes findings, evidence, suggestions and a submission ID. If `OPENAI_API_KEY` is configured, an additional cautious AI review runs; deterministic checks work without it.

## 4. Review an image
`POST /api/brands/{brand_id}/assets/logo` — multipart fields: `name`, `file`.
`POST /api/brands/{brand_id}/review/image` — multipart fields: `file`, optional `alt_text`.

The MVP compares perceptual hashes against uploaded approved logos, checks image dimensions and missing alt text. It does not claim full OCR or semantic image understanding.

## 5. Human workflow
- `GET /api/submissions`
- `GET /api/submissions/{submission_id}`
- `POST /api/submissions/{submission_id}/revise` — automatically reruns checks.
- `POST /api/submissions/{submission_id}/decision` with action `approve`, `request_changes`, or `comment`.
- Set `REVIEWER_API_KEY` and send it as `X-Reviewer-Key` to protect decisions.

## 6. Analytics and automation
- `GET /api/brands/{brand_id}/analytics`
- `GET /api/automation/status`

Automations currently include review on submission, re-review after revisions, and recurring-issue aggregation. Scheduled reminders require a separate scheduler/worker and are not claimed as implemented.

## Security / demo limitations
This is a functional MVP foundation, not a production-hardened multi-tenant SaaS. Public demo endpoints do not implement user login or tenant isolation. Use synthetic demo data only until authentication, per-tenant authorization, private object storage, retention controls, rate limiting, malware scanning and backups are configured. Do not send confidential materials to an external AI provider without organisational approval. Human approval is mandatory. Disclose all AI/API/library usage and build-window timing accurately.
