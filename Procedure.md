---
title: "Procedure"
---

# Yellowbook Procedure Guide

Энэ баримт нь төслийн хүрээнд байнга давтагддаг үндсэн үйлдлүүдийг (журам) алхамчилсан байдлаар жагсаана.

## 1. Локал хөгжүүлэлтийн орчин асаах журам

1. Repository-г шинэчлэх
   ```bash
   git pull origin main
   ```
2. Dependencies шинэчлэх (шаардлагатай бол)
   ```bash
   npm install
   ```
3. Database migration + seed хийх
   ```bash
   npx prisma migrate dev
   npm run db:seed
   ```
4. API сервер асаах
   ```bash
   npx nx serve api
   ```
5. Web (Frontend) асаах
   ```bash
   npx nx serve web
   ```

## 2. Тест ажиллуулах журам

1. Lint шалгах
   ```bash
   npx nx run-many -t lint
   ```
2. Unit тест ажиллуулах
   ```bash
   npx nx run-many -t test
   ```
3. Build шалгах
   ```bash
   npx nx run-many -t build
   ```
4. E2E тест ажиллуулах
   ```bash
   npx nx e2e web-e2e
   ```

## 3. Docker-оор локал тест хийх журам

1. Docker Desktop асаалттай эсэхийг шалгах
2. Төслийн root хавтас руу орох
   ```bash
   cd yellowbook
   ```
3. Docker Compose-оор бүх зүйл асаах
   ```bash
   docker-compose up --build
   ```
4. Web болон API-г шалгах
   - Web: http://localhost:3000
   - API: http://localhost:3333
5. Ажлаад дууссаны дараа зогсоох
   ```bash
   docker-compose down
   ```

Дэлгэрэнгүй: `docs/LOCAL-TESTING.md`.

## 4. Шинэ фичер хөгжүүлэх ерөнхий журам

1. Issue/feature-ээ тодорхойлох (ямар API, ямар UI өөрчлөх г.м.)
2. Шинэ branch үүсгэх
   ```bash
   git checkout -b feature/<short-name>
   ```
3. Contract (libs/contract) өөрчлөх шаардлагатай эсэхийг шалгах
4. API (`apps/api`) дээр шаардлагатай endpoint-үүдийг нэмэх/засах
5. Web (`apps/web`) дээр UI болон data fetch хэсгийг өөрчлөх
6. Тестүүдийг шинэчлэх/нэмэх (хэрвээ боломжтой бол)
7. Lint + тестүүдийг локал дээр ажиллуулж ногоон болгох
8. Commit хийх
   ```bash
   git commit -m "feat: ..."
   ```
9. Remote руу push хийж, Pull Request нээх

## 5. CI/CD-ээр deploy хийх ерөнхий журам

1. Main branch руу merge хийхээс өмнө бүх тест ногоон болсон эсэхийг шалгах
2. Main руу merge хийсний дараа GitHub Actions-ийг хянах
3. Хэрэв AWS EKS deployment тохирсон бол:
   - Docker images ECR рүү push болсон эсэх
   - Kubernetes manifests амжилттай apply болсон эсэх
4. Live орчин дээр апп ажиллаж байгаа эсэхийг шалгах (Ingress хаяг руу орж)