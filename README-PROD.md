# Production Bundle

## Build & Push Images (GitHub Actions)
1. Set repository to **public** or enable GHCR for your account.
2. Push to `main` — the workflow `.github/workflows/docker-publish.yml` builds:
   - `ghcr.io/<OWNER>/fm-api:latest`
   - `ghcr.io/<OWNER>/fm-web:latest`

## Deploy
1. Replace `OWNER` in `docker-compose.prod.yml` with your org/user.
2. Provide certs at `./certs` (or edit `nginx/prod.conf` to use Let's Encrypt).
3. On your server:
```bash
git clone <repo>
cd repo
cp .env.example .env
docker compose -f docker-compose.prod.yml up -d
```

- Web served by Nginx static container.
- API proxied at `/api/` with websocket upgrade.
- Mongo + Redis run as services; mount volumes as needed.

## Environment
- `PI_ENV=mock` for sandbox (default). Switch to real adapter in `apps/api/src/payments/pi.adapter.ts` when ready.
- `CORS_ORIGIN` should include your production domain (comma-separated if multiple).

## Hardening
- API Docker runs as non-root user.
- Nginx enables gzip and security headers.
- Rate limiting & Helmet enabled in Express.
- Keep `JWT_SECRET` strong and rotated.
