---
title: "Reference"
---

# Yellowbook Reference Guide

Энэ баримт нь төслийн гол лавлах мэдээллүүдийг (командууд, env хувьсагч, API endpoint-ууд г.м.) нэг дороос харах зорилготой.

## 1. NPM/Nx командууд

### Ерөнхий

- Install dependencies
  ```bash
  npm install
  ```
- Lint
  ```bash
  npx nx run-many -t lint
  ```
- Test
  ```bash
  npx nx run-many -t test
  ```
- Build
  ```bash
  npx nx run-many -t build
  ```
- E2E тест
  ```bash
  npx nx e2e web-e2e
  ```

### API

- Serve API
  ```bash
  npx nx serve api
  ```

### Web

- Serve Web
  ```bash
  npx nx serve web
  ```

## 2. Environment хувьсагчууд

Root `.env` файлд ашиглагдах үндсэн хувьсагчууд:

```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/yellowbook"
PORT=3333
NEXT_PUBLIC_API_URL="http://localhost:3333"
```

AWS/EKS deployment үед нэмэгдэх боломжтой хувьсагчуудын жишээ:

- `DATABASE_URL`  Production/Postgres connection string
- `PORT`  API-ийн порт
- `NEXT_PUBLIC_API_URL`  Frontend-ээс харах API URL

## 3. API Endpoint Reference

Эдгээр нь үндсэн Yellowbook API endpoint-уудын жишээ (Express + Prisma):

### Public endpoints

- `GET /`  API эрүүл эсэх, үндсэн мэдээлэл
- `GET /yellow-books`  Бүх бизнесийн жагсаалт авах (хэн ч харж болно)
- `GET /yellow-books/:id`  Тодорхой бизнесийн мэдээлэл авах
- `POST /api/ai/yellow-books/search`  AI semantic search (Gemini)
  - Request body: `{ "query": "coffee shop" }`

### Admin-only endpoints (Authentication шаардлагатай)

- `POST /api/yellow-books`  Шинэ бизнес үүсгэх (ADMIN л хийнэ)
  - Header: `Authorization: Bearer admin@yellowbook.mn`
  - Request body жишээ:
    ```json
    {
      "businessName": "Test Business",
      "category": "Technology",
      "phoneNumber": "99119911",
      "address": "Ulaanbaatar, Mongolia"
    }
    ```
- `DELETE /api/yellow-books/:id`  Бизнес устгах (ADMIN л хийнэ)
  - Header: `Authorization: Bearer admin@yellowbook.mn`

### Admin хэрэглэгч

Үндсэн админ: `admin@yellowbook.mn` (role: ADMIN)

Дэлгэрэнгүй endpoint-уудыг `apps/api/src/main.ts` файлаас харж болно.

## 4. Төслийн бүтэц (линк лавлах)

- apps/api  Express backend
- apps/web  Next.js frontend
- apps/web-e2e  Playwright E2E тест
- libs/contract  Shared Zod схемүүд
- libs/config  Shared configuration
- prisma  Database schema, migrations, seed
- k8s  Kubernetes manifests (Deployment, Service, Ingress гэх мэт)

## 5. Docker/Lokal тесттэй холбоотой лавлах

Холбогдох дэлгэрэнгүй баримтууд:

- Local Docker тест: `docs/LOCAL-TESTING.md`
- AWS ECR тохиргоо: `docs/AWS-ECR-SETUP.md`
- EKS архитектур: `ARCHITECTURE.md`
- K8s manifests тайлбар: `k8s/README.md`
