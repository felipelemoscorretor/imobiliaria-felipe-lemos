# CI/CD & Deployment - Felipe Lemos

## GitHub Secrets (set these in your repository settings)
- VERCEL_TOKEN
- VERCEL_ORG_ID
- VERCEL_PROJECT_ID
- DOCKERHUB_USER
- DOCKERHUB_TOKEN
- DO_API_TOKEN (optional, for DigitalOcean)
- DO_APP_ID (optional)
- DATABASE_URL
- JWT_SECRET

## Quick steps to enable automatic deploys
1. Push this repo to GitHub.
2. Add the secrets above (Settings -> Secrets -> Actions).
3. For Vercel: create a Vercel project linked to this repo; get ORG_ID and PROJECT_ID.
4. For DigitalOcean: create an App that uses the Docker images or use `app_spec.yaml` to create via API.
5. On push to `main`, GitHub Actions will:
   - Build & deploy the frontend to Vercel.
   - Build Docker image for backend, push to Docker Hub, and trigger DO deployment (if configured).

## Manual deploy with Docker Compose (VPS)
1. Install Docker & Docker Compose on the server.
2. Copy repo to server.
3. Run: `docker-compose up --build -d`
4. Then run migrations and seed inside the API container:
   - `docker exec -it <api_container> npm run prisma:migrate`
   - `docker exec -it <api_container> npm run seed`
