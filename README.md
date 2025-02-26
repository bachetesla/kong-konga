# Kong & Konga Docker Setup

## Overview
This Docker Compose setup deploys Kong API Gateway with PostgreSQL as its database and Konga as the UI to manage Kong. On the first run, Konga should be started in development mode.

## Prerequisites
Ensure you have the following installed on your system:
- Docker
- Docker Compose

## Services

### 1. PostgreSQL Database (`kong-database`)
- Stores Kong and Konga data.
- Includes health checks.

### 2. Kong Migrations (`kong-migrations`)
- Initializes the database for Kong.
- Runs the necessary migrations.

### 3. Kong API Gateway (`kong`)
- The main Kong service for API gateway functionality.
- Exposes ports for proxy (`8000`) and admin API (`8001`).

### 4. Konga UI (`konga`)
- A web UI to manage Kong.
- Runs on port `1337`.
- Starts in **development mode** on first run.

## First-Time Setup
On the first run, Konga should be started in **development mode** to initialize the database.

1. Run the following command to start the services:
   ```sh
   docker-compose up -d
   ```

2. Manually start Konga in development mode (only for the first run):
   ```sh
   docker-compose exec konga node ./bin/konga.js --dev
   ```
   This initializes the database for Konga. After initialization, restart Konga in production mode:
   ```sh
   docker-compose restart konga
   ```

## Usage
Once all services are running:
- Kong Admin API: `http://localhost:8001`
- Kong Proxy: `http://localhost:8000`
- Konga UI: `http://localhost:1337`

Login to Konga and connect it to Kong by providing the Kong Admin API URL (`http://kong:8001`).

## Stopping the Services
To stop all running containers:
```sh
docker-compose down
```

To restart the services:
```sh
docker-compose up -d
```

## Logs
To view logs for a specific service, use:
```sh
docker-compose logs -f <service_name>
```
For example, to check Kong logs:
```sh
docker-compose logs -f kong
```

## Troubleshooting
- If Kong fails to start, ensure the database migrations were applied correctly.
- If Konga fails to connect, verify that the database settings are correct.

## Credits
This setup is based on official Kong and Konga Docker images.