# QiTarot Deployment Checklist

## Supabase

- [ ] Run `supabase/migrations/001_qitarot.sql`.
- [ ] Run `supabase/migrations/20260706100441_qitarot_catalog_people_analytics.sql`.
- [ ] Confirm `qitarot_` tables exist.
- [ ] Confirm `qitarot_cards` has 78 rows.
- [ ] Confirm `qitarot_people` exists.
- [ ] Confirm spread seed rows exist in `qitarot_spread_templates`.
- [ ] Confirm storage bucket `qitarot-reading-photos` exists.
- [ ] Confirm frontend cannot write directly to protected tables.

## Cloudflare Worker

- [ ] Project name: `qitarot-api`.
- [ ] Root directory: `apps/qitarot-api`.
- [ ] Deploy command: `npx wrangler deploy`.
- [ ] Entry file: `src/index.ts`.
- [ ] Custom domain: `tarot.askcody.me` (or `api.tarot.askcody.me`).
- [ ] Set secrets: `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`, `OPENAI_API_KEY`.
- [ ] Set vars: `CORS_ORIGIN=https://tarot.askcody.me`, `QITAROT_APP_SLUG=qitarot`.
- [ ] Hit `https://tarot.askcody.me/v1/qitarot/health`.

## Cloudflare Pages

- [ ] Project name: `qitarot-web`.
- [ ] Root directory: `apps/qitarot-web`.
- [ ] Build command: `npm run build`.
- [ ] Output directory: `dist`.
- [ ] Custom domain: `tarot.askcody.me`.
- [ ] Set `VITE_QITAROT_API_BASE_URL=https://tarot.askcody.me`.
- [ ] Set `VITE_QITAROT_APP_SLUG=qitarot`.

## Production Sanity

- [ ] No Supabase service keys in frontend build.
- [ ] No direct browser calls to Supabase REST.
- [ ] CORS does not use `*` in production.
- [ ] Create a test reading.
- [ ] Upload a test image.
- [ ] Confirm reading appears in timeline after refresh.
- [ ] Failed OCR/AI jobs return clean status, not broken UI.
