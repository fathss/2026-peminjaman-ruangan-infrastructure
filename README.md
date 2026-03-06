# Infrastructure Setup

Panduan utama menjalankan sistem menggunakan Docker Compose.

## Arsitektur

- Backend: ASP.NET 10
- Frontend: React + Vite + Nginx
- Database: Supabase (external)

## Quick Setup Via Docker

### 1. Pastikan Docker aktif

```powershell
docker --version
docker compose version
```

### 2. Jalankan dari folder `infrastructure`

```powershell
docker compose -f compose.yaml pull
docker compose -f compose.yaml up -d
```

### 3. Akses aplikasi

- Frontend: `http://localhost:3000`
- Backend API: `http://localhost:5000`

### 4. Cek status dan logs

```powershell
docker compose -f compose.yaml ps
docker compose -f compose.yaml logs -f
```

### 5. Stop service

```powershell
docker compose -f compose.yaml down
```

## Catatan

- Compose file ini tidak menjalankan PostgreSQL lokal.
- Connection string Supabase dibaca dari `backend/PeminjamanRuangan.API/appsettings.json` di image backend.
- Port mapping backend adalah `5000:8080`.

## Alternatif Manual (Tanpa Docker)

Jika ingin menjalankan service satu per satu:

1. Jalankan backend dari [2026-peminjaman-ruangan-backend](https://github.com/fathss/2026-peminjaman-ruangan-backend.git) dengan `dotnet run`.
2. Jalankan frontend dari repositori [2026-peminjaman-ruangan-frontend](https://github.com/fathss/2026-peminjaman-ruangan-frontend.git) dengan `npm run dev`.
