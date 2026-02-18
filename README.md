# RabbitMQ

![Docker](https://img.shields.io/badge/docker-ready-blue)

Install RabbitMQ with management UI using Docker

## Table of Contents

- [Requirements](#requirements)
- [Quick Start](#quick-start)
- [Access UI](#access-ui)
- [Configuration](#configuration)
- [Security](#security)

## Requirements

- Docker
- Docker Compose
- Docker network (must be created beforehand)

## Quick Start

### 1. Create Docker Network

Before running RabbitMQ, create a Docker network:

```bash
docker network create <name>
```
example:
```bash
docker network create net
```

### 2. Clone Repository

```bash
git clone https://github.com/alfattd/rabbitmq.git
```

### 3. Setup Environment

Copy the `.env.example` file to `.env` and customize the configuration if needed:

```bash
cp .env.example .env
```

Default configuration:
```env
RABBITMQ_USER=rabbitmq
RABBITMQ_PASSWORD=rabbitmq
NETWORK=net
```

### 4. Run RabbitMQ

```bash
docker-compose up -d
```

## Access UI

Once the container is running, access the management UI through your browser:

- **URL:** http://localhost:15672
- **Username:** `rabbitmq` (default or as per `.env`)
- **Password:** `rabbitmq` (default or as per `.env`)

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `RABBITMQ_USER` | RabbitMQ username | `rabbitmq` |
| `RABBITMQ_PASSWORD` | RabbitMQ password | `rabbitmq` |
| `NETWORK` | Docker network name | `net` |

### Ports

- **15672:** RabbitMQ Management UI (HTTP)
- **5672:** AMQP Protocol (default, not exposed)

### Volumes

- `data:/var/lib/rabbitmq` - Persistent storage for RabbitMQ data

## Security

**Important Notes:**
- Do not use default credentials (`rabbitmq`) in production
- Replace username and password in `.env` file with strong credentials
- Never commit `.env` file to repository (already in `.gitignore`)

## Application Connection

To connect your application to RabbitMQ:

```
Host: rabbitmq (if in the same network)
Port: 5672
Username: (as per RABBITMQ_USER)
Password: (as per RABBITMQ_PASSWORD)
```

Example connection string:
```
amqp://rabbitmq:rabbitmq@rabbitmq:5672/
```
