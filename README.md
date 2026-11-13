# Render deployment assignment

The Express and Prisma demo for this assignment is in [`lu63-render-demo/`](./lu63-render-demo/). A root-level [`render.yaml`](./render.yaml) describes the service using the assignment's required settings, so Render can provision it as a Blueprint.

## Render service settings

If configuring the service manually, connect your personal GitHub fork and use:

- **Root Directory:** `lu63-render-demo`
- **Build Command:** `npm ci && npx prisma generate`
- **Start Command:** `node server.js`
- **Instance Type:** Free
- **Environment Variable:** `NODE_ENV=production`

Do not set `PORT` manually. Render supplies it at runtime; the server reads `process.env.PORT` and falls back to `5000` for local development. Do not commit a `.env` file or database credentials. The `/health` endpoint does not need a database. The `/api/notes` endpoint needs a valid PostgreSQL `DATABASE_URL` configured in Render's Environment section.

## Verify the deployment

After the first deploy succeeds, open `https://<your-service>.onrender.com/health`. A healthy response is:

```json
{"status":"ok"}
```

The Render deploy log should show a successful Prisma Client generation, a successful build, the server listening on Render's injected port, and a live-service URL. On the Free plan, an idle service can spin down; its next request may take longer while it starts again.

## References

- [Render Blueprint YAML reference](https://render.com/docs/blueprint-spec)
- [Render web services](https://render.com/docs/web-services)
