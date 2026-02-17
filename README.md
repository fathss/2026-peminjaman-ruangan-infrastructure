# Infrastructure Setup

## PeminjamanRuangan System

Repository ini berisi panduan instalasi dan konfigurasi environment untuk menjalankan sistem **Peminjaman Ruangan Kampus** secara manual.

---

# Arsitektur Sistem

Sistem terdiri dari:

* **Backend**: ASP.NET 10
* **Frontend**: React + TypeScript (Node.js)
* **Database**: PostgreSQL

---

# 🔧 Requirements

Pastikan sudah menginstall:

## 1. .NET 10 SDK

Download:
https://dotnet.microsoft.com/download

Cek versi:

```
dotnet --version
```

---

## 2️. Node.js (LTS)

Download:
https://nodejs.org

Cek versi:

```
node -v
npm -v
```

---

## 3. PostgreSQL

Download:
https://www.postgresql.org/download/

Pastikan `psql` dapat diakses:

```
psql --version
```

---

# Backend Configuration (ASP.NET)

Masuk ke repository backend.

## 1. Install Dependency

```
dotnet restore
```

## 2. Setup appsettings.json

Edit:

```
appsettings.json
```

Tambahkan connection string dan jwt:

```json
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=PeminjamanRuanganDB;Username=postgres;Password=PASSWORD"
  },

  "Jwt": {
    "Key": "MINIMAL_32_KARAKTER_RAHASIA",
    "Issuer": "PeminjamanRuanganAPI",
    "Audience": "PeminjamanRuanganApp"
  },
```

## 3️. Jalankan Migration

```
dotnet ef database update
```

Jika belum ada migration:

```
dotnet ef migrations add InitialCreate
dotnet ef database update
```

## 4️. Jalankan Backend

```
dotnet run
```

---

# Frontend Setup (React + TypeScript)

Masuk ke repository frontend.

## 1️. Install dependency

```
npm install
```

## 2️. Pastikan BASE URL API

Ambil Contoh dari file

```
env.example
```

Pastikan port localhost sesuai dengan localhost backend masing-masing:

```ts
VITE_API_URL=http://localhost:5001/api
```

## 3️. Jalankan Frontend

```
npm run dev
```

---

# CORS Configuration (Backend)

Pastikan backend mengizinkan frontend:
Di file `Program.cs`,
```csharp
builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowFrontend",
        policy =>
        {
            policy.WithOrigins("http://localhost:5100")
                  .AllowAnyHeader()
                  .AllowAnyMethod();
        });
});

app.UseCors("AllowFrontend");
```

*Pastikan port localhost sama dengan localhost frontend masing-masing

---

# Menjalankan Sistem Secara Lengkap

1. Jalankan PostgreSQL
2. Jalankan Backend (`dotnet run`)
3. Jalankan Frontend (`npm run dev`)

---
