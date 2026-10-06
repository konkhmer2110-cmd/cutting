# Fabric Cutting System — iPhone / Production Deployment

## What is included
- React + Vite frontend
- Express API served from the same domain in production
- PostgreSQL connection via `DATABASE_URL`
- HTTPS-ready deployment on Render/Railway/etc.
- Login with signed tokens and scrypt password hashing
- PWA manifest + Apple touch icon for iPhone Home Screen
- Mobile-safe UI and API authentication

## Local test
```bash
npm install
cp .env.example .env
# edit DATABASE_URL and ADMIN_PASSWORD
npm run db:init
npm run dev
```

For a production-style local server:
```bash
npm run build
npm start
```
Open `http://localhost:4000`.

## Render
1. Create a PostgreSQL database in Render (or use another hosted PostgreSQL provider).
2. Create a Web Service from this repository/ZIP after uploading it to your Git provider.
3. Use Docker runtime; the included `Dockerfile` builds and serves the app.
4. Set these environment variables:
   - `DATABASE_URL` = your PostgreSQL connection string
   - `DATABASE_SSL=true`
   - `JWT_SECRET` = long random secret
   - `ADMIN_USERNAME` = desired first admin username
   - `ADMIN_PASSWORD` = strong first admin password
   - `ADMIN_EMPLOYEE_ID=ADMIN001`
   - `ADMIN_NAME=System Administrator`
5. After the database is reachable, run once:
   `npm run db:init`
   If your host supports a pre-deploy command, set it to `npm run db:init`.
6. Open the HTTPS URL on iPhone Safari and choose **Share → Add to Home Screen**.

## Important
Do not put `DATABASE_URL`, `JWT_SECRET`, or `ADMIN_PASSWORD` in frontend code. They must remain server environment variables.


## Version 2 checklist

1. Set a strong `JWT_SECRET`.
2. Set `ADMIN_USERNAME`, `ADMIN_PASSWORD`, `ADMIN_EMPLOYEE_ID`, and `ADMIN_NAME`.
3. Run `npm run db:init`.
4. Deploy with `NODE_ENV=production`.
5. Sign in as ADMIN and create Supervisor/QC/Store/Viewer accounts from **Settings → User Management**.
6. Keep `DATABASE_URL` and passwords only in the hosting provider's environment variables.
