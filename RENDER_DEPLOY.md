# 🚀 Render Deployment Guide for Freelance Marketplace

## Prerequisites
- A GitHub repo containing the full project (steps 1–12).
- A [Render](https://render.com) account.

## Steps

1. **Add `render.yaml` to your repo root.**
   ```bash
   cp render.yaml <your-repo>/render.yaml
   git add render.yaml
   git commit -m "Add Render deployment config"
   git push origin main
   ```

2. **On Render dashboard → Blueprints → New Blueprint Instance.**
   - Connect your GitHub repo.
   - Choose branch (usually `main`).

3. **Render will provision:**
   - `freelance-web` (React static site).
   - `freelance-api` (Node backend).
   - `freelance-mongo` (managed MongoDB).
   - `freelance-redis` (managed Redis).

4. **Configure Environment Variables (API Service):**
   - `MONGO_URI` → value from Render's Mongo connection string.
   - `REDIS_URL` → value from Render's Redis connection string.
   - `JWT_SECRET` → any strong secret string.
   - `PI_ENV` → `mock` (switch later if using real Pi SDK).
   - `CORS_ORIGIN` → `https://<your-web-app>.onrender.com`.

5. **Deployment URLs**
   - Frontend → `https://freelance-web.onrender.com`
   - Backend → `https://freelance-api.onrender.com/api`

6. **Update frontend API URL**
   - In `render.yaml`, `VITE_API_URL` is set to `https://freelance-api.onrender.com/api`.
   - Change it if using custom domains.

7. **Redeploy**
   - Web redeploys automatically on code push.
   - API redeploys automatically on code push.

## Optional
- Add a custom domain via Render → Custom Domains.
- Enable auto-scaling if traffic grows.

---
You're now live on Render 🚀
