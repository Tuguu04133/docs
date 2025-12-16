---
title: "Tutorial"
---

# Yellowbook Tutorial

Энэ tutorial нь Yellowbook (Монголын Бизнес Лавлах) төслийг эхнээс нь клон хийж, локал дээрээ ажиллуулах хүртэл алхамчилсан байдлаар тайлбарлана.

## 1. Урьдчилсан шаардлага

Танд дараах програмууд суусан байх хэрэгтэй:

- Node.js 20.x
- npm
- Git
- Docker Desktop (заавал биш, Docker-оор ажиллуулах бол)

## 2. Repo-ийг клон хийх

```bash
git clone https://github.com/Tuguu04133/yellowbook.git
cd yellowbook
```

## 3. Dependencies суулгах

```bash
npm install
```

Суулгалт амжилттай болсны дараа Nx, Next.js, Express, Prisma гэх мэт хэрэгтэй бүх dependency суусан байна.

## 4. Environment тохиргоо хийх

Төслийн root дээр `.env` файл үүсгээд дараах утгуудыг оруулна:

```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/yellowbook"
PORT=3333
NEXT_PUBLIC_API_URL="http://localhost:3333"
```

Дараа нь Prisma schema-аас database-ээ бэлдэнэ:

```bash
npx prisma generate
npx prisma migrate dev
npm run db:seed
```

## 5. Backend (API) ажиллуулах

```bash
npx nx serve api
```

Амжилттай ажилласан бол:

- API: http://localhost:3333

Browser эсвэл `curl` ашиглаж шалгаж болно:

```bash
curl http://localhost:3333/
```

## 6. Frontend (Web) ажиллуулах

Шинэ terminal нээж дараах командыг өгнө:

```bash
npx nx serve web
```

Амжилттай бол:

- Web: http://localhost:4200

Browser-оор http://localhost:4200 хаяг руу орж Yellowbook UI-г харна.

## 7. Docker ашиглаж түргэн турших (сонголтоор)

Хэрэв Docker-оор түргэн асаахыг хүсвэл:

```bash
# Build + run
docker-compose up --build

# Background дээр
docker-compose up -d --build
```

Хаягууд:

- Web: http://localhost:3000
- API: http://localhost:3333

Дэлгэрэнгүй зааврыг `docs/LOCAL-TESTING.md`-ээс үзэж болно.

## 8. Тестүүд ажиллуулах

```bash
# Lint
npx nx run-many -t lint

# Unit тест
npx nx run-many -t test

# E2E
npx nx e2e web-e2e
```

## 9. Дараагийн алхам

- Кодын бүтцийг ойлгох: `README.md`-ийн "Project бүтэц" хэсэг
- AWS/EKS deployment сонирхож байвал: `k8s/README.md` болон `ARCHITECTURE.md`