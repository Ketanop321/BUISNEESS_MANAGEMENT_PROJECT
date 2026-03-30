# Deployment Guide

## Reality Check About Vercel
This project is a Spring Boot server-rendered app (Thymeleaf + Java backend + DB).

- Vercel is great for frontend frameworks and serverless functions.
- Running this full Java Spring Boot app with persistent DB directly on Vercel is not the professional path.
- Vercel also does not provide managed MySQL DB hosting.

Professional approach:
- Frontend: Vercel (only if you split frontend separately)
- Backend: Render or Railway (Spring Boot service)
- Database: Neon, PlanetScale, Railway MySQL, Aiven, or AWS RDS

## Recommended Fast Path (Railway or Render)

### 1) Backend Service
- Connect your GitHub repo.
- Build command: `./mvnw -DskipTests clean package`
- Start command: `java -Dspring.profiles.active=prod -jar target/BusinessProject-0.0.1-SNAPSHOT.jar`

### 2) Environment Variables
Set these in the backend host:
- `SPRING_DATASOURCE_URL`
- `SPRING_DATASOURCE_USERNAME`
- `SPRING_DATASOURCE_PASSWORD`
- `PORT` (usually auto-provided)

### 3) Database
Provision a managed MySQL-compatible database and copy connection values into env vars above.

### 4) Verify
After deploy, open:
- `/home`
- `/login`
- `/products`

## If You Still Want Vercel
Use Vercel only after splitting this into:
- Frontend app (React/Next.js) on Vercel
- Backend API (Spring Boot) on Render/Railway
- DB in managed service
