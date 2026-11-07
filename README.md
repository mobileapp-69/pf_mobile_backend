# Preflight Mobile Backend

## Database Setup

- `pnpm install`
- Create `.env` from `.env.example`
- DB container
  - `pnpm run eol` to set the correct line endings (Windows)
  - `chmod +x ./scripts/*.sh` to make scripts executable (Linux/Mac)
  - `docker compose --env-file ./.env -f docker-compose-db.yml up -d` to start the database
- Remove DB container (with volume)
  - `docker compose --env-file ./.env -f docker-compose-db.yml down -v`

## Drizzle Setup

- `pnpm run db:push`
- `pnpm run db:generate`
- `pnpm run db:migrate`
- `pnpm run db:prototype`

# Setup Express.js Backend

- Make sure that you already have DB running
- `pnpm run dev`

# Cloudflare Tunnel

- Fill in the `.env` file with your Cloudflare Tunnel credentials
- Start the container
  - `docker compose --env-file ./.env -f docker-compose-tunnel.yml up -d`
- Remove the container
  - `docker compose --env-file ./.env -f docker-compose-tunnel.yml down`

# Containerization (Express.js appplication) and test

- Generate migration (if you have not done so)
  - `pnpm run db:generate`
- Make `.env.test` from `.env.test.example`
- Build the backend and start containers (backend and tunnel)
  - `docker compose --env-file ./.env.test -f docker-compose-test.yml up -d --force-recreate --build`
- Start the backend and tunnel (no build)
  - `docker compose --env-file ./.env.test -f docker-compose-test.yml up -d --force-recreate`
- Remove the containers
  - `docker compose --env-file ./.env.test -f docker-compose-test.yml down`

# Push to dockerhub

- `docker tag preflight_mobile_backend [DOCKERHUB_ACCOUNT]/preflight_mobile_backend:latest`
- `docker push [DOCKERHUB_ACCOUNT]/preflight_mobile_backend:latest`
