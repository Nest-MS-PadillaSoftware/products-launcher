# ProductsApp microservices

Example project with a NestJS-based microservices architecture.

## Overview

The application is composed of three main services and a message broker:

- `client-gateway`: HTTP gateway that exposes REST endpoints and consumes the microservices.
- `products-ms`: products microservice with persistence in SQLite (`dev.db`).
- `order-ms`: orders microservice with persistence in PostgreSQL.
- `nats-server`: NATS message broker for communication between services.

The main orchestration file is `docker-compose.yml`, which brings up all services together.

## Technologies

- NestJS
- NATS
- PostgreSQL
- SQLite
- Prisma
- TypeScript

## Repository structure

- `client-gateway/` — HTTP gateway and microservices client.
- `products-ms/` — products microservice.
- `order-ms/` — orders microservice.
- `docker-compose.yml` — development container configuration.

## How to run

From the repository root:

```bash
docker compose up --build
```

This will start:

- `nats-server` on ports `4222` and `8222`
- `client-gateway` on port `3000`
- `products-ms` on port `3001`
- `order-ms` on port `3002`
- `orders-db` on port `5433`

## Exposed ports

- `http://localhost:3000` — REST gateway
- `http://localhost:3001` — products microservice
- `http://localhost:3002` — orders microservice
- `http://localhost:8222` — NATS console
- `localhost:5433` — PostgreSQL for `order-ms`

## Detailed services

### client-gateway

- Exposes REST endpoints to manage products.
- Communicates with microservices via `NATS`.
- Directory: `client-gateway/`
- Service README: `client-gateway/README.md`

### products-ms

- Products microservice.
- Uses `Prisma` and SQLite.
- Directory: `products-ms/`
- Service README: `products-ms/README.md`

### order-ms

- Orders microservice.
- Uses PostgreSQL as its database.
- Directory: `order-ms/`
- Service README: `order-ms/README.md`

## Environment variables

The services use variables defined in `docker-compose.yml`:

- `CLIENT_GATEWAY_PORT` — gateway port.
- `PORT` — service port.
- `NATS_SERVERS` — NATS broker URL.
- `DATABASE_URL` — database connection string.

## Useful commands

Run only the gateway:

```bash
cd client-gateway
npm install
npm run dev
```

Run only the products microservice:

```bash
cd products-ms
npm install
npx prisma generate
npm run dev
```

Run only the orders microservice:

```bash
cd order-ms
npm install
npm run dev
```

## Development and testing

Each service has its own npm scripts and README with detailed instructions. If you run locally without Docker, check each service README for environment setup and specific commands.

## Final notes

- This is an early-stage microservices base.
- The gateway depends on `products-ms` and `order-ms` being available.
- Adjust environment variables and ports according to your local setup.

---

Built for the `ProductsApp` project with a microservices-oriented architecture.