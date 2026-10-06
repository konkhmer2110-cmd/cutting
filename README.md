# Fabric Cutting System

Mobile-ready React/Vite + Express + PostgreSQL production management app.

## Quick start
```bash
npm install
cp .env.example .env
# edit DATABASE_URL and ADMIN_PASSWORD
npm run db:init
npm run dev
```

## Production
```bash
npm run build
npm start
```

The production server serves both the React app and `/api` from the same HTTPS domain, so iPhone Safari does not need a separate frontend API URL.

See `DEPLOYMENT.md` for hosted PostgreSQL, HTTPS, Render, and iPhone Home Screen setup.


## Version 2 — Roles & User Management

Roles supported by the application:
- ADMIN — full access, user management
- SUPERVISOR — production and operational write access
- QC — quality records
- STORE — fabric stock
- VIEWER — read-only access

The Settings → User Management screen is available to ADMIN only. It supports create, edit, deactivate and delete for system accounts. Passwords are stored as scrypt hashes and API routes enforce role permissions server-side.

### Database
Run `npm run db:init` once with `DATABASE_URL` and `ADMIN_PASSWORD` configured. Existing databases are not overwritten.

## Version 3.1 Administration
- Permission Matrix stored in PostgreSQL and enforced on authenticated API routes.
- Audit Log records authenticated CRUD/report/security API activity.
- JSON database backup and restore from the Admin Tools UI.
- Excel (`.xlsx`) and PDF report exports for production, fabric, quality and workers.
- Admin navigation: Permission Matrix, Audit Log, Report Center, Backup / Restore.

Run after upgrading:

```bash
npm install
npm run db:init
npm run build
npm start
```
