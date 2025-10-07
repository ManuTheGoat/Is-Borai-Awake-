# is @borai awake? (Vercel + KV)

This repo hosts a globally synced status page. The status is stored server-side in Vercel KV (Redis) and flipped via a serverless function protected by a secret.

## Files
- `index.html` – client UI
- `api/status.ts` – serverless API (Node on Vercel) that reads/writes the shared status
- `package.json` – minimal Node project
- `.gitignore` – ignore env and node_modules

## One-time setup on Vercel
1. **Create project** and link this repo.
2. **Add Vercel KV (Upstash)** via Vercel Marketplace and link it to this project.
3. **Set env var** `SECRET_PIN` (e.g., `3141592653589`) in Project → Settings → Environment Variables.
4. Deploy.

## Endpoints
- `GET /api/status` → `{ status: 'yes'|'no', bedISO?, wakeISO?, updatedAtISO }`
- `POST /api/status` with JSON `{ action: 'sleep'|'wake', secret: '<pin>' }`

## Local dev (optional)
```bash
npm install
npm run dev
```
Pull your env vars with `vercel env pull` if you want to test POST locally.
