# RouteHound Backend

> API observability backend for RouteHound — captures request telemetry from Express applications and provides real-time monitoring, error tracking, endpoint performance analytics, and p50/p95 latency insights.

---

## Tech Stack

| Layer                   | Technology |
| ----------------------- | ---------- |
| Runtime                 | Node.js    |
| Framework               | Express.js |
| ORM                     | Sequelize  |
| Database                | MySQL      |
| Auth                    | JWT        |
| Real-Time Communication | Socket.IO  |

---

## Features

* **Project management** — create and manage multiple applications from a single account
* **API key authentication** — project-specific API keys for securely ingesting telemetry from connected applications
* **Request telemetry** — capture endpoints, HTTP methods, status codes, response times, errors, and timestamps
* **Real-time monitoring** — stream incoming request activity to connected dashboards through Socket.IO
* **Request history** — store and retrieve historical API requests for debugging and investigation
* **Search and filtering** — query requests by endpoint, HTTP method, status code, error state, and date range
* **Error tracking** — identify failed requests, recurring errors, and endpoints with high failure rates
* **API analytics** — calculate request volume, error rates, average response times, and overall API health
* **Endpoint performance** — aggregate request count, response time, and error metrics for individual endpoints
* **Latency analytics** — calculate p50 and p95 latency to expose typical performance and slow request spikes
* **Multi-project isolation** — keep telemetry, analytics, API keys, and live request streams isolated per project

---

## Getting Started

### Prerequisites

* Node.js >= 18
* MySQL >= 8

### Installation

```bash
git clone https://github.com/snageshprasad/route-hound-backend.git
cd route-hound-backend
npm install
```

### Environment Setup

```bash
cp .env.example .env
```

Fill in your `.env`:

```env
PORT=5000

DB_HOST=localhost
DB_PORT=3306
DB_NAME=routehound
DB_USER=root
DB_PASSWORD=your_password

JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d

FRONTEND_URL=http://localhost:5173
```

### Run

```bash
# development
npm run dev

# production
npm start
```

---

## Environment Variables

| Variable         | Required | Description                                    |
| ---------------- | -------- | ---------------------------------------------- |
| `PORT`           | No       | Server port (default: 5000)                    |
| `DB_HOST`        | Yes      | MySQL host                                     |
| `DB_PORT`        | No       | MySQL port (default: 3306)                     |
| `DB_NAME`        | Yes      | Database name                                  |
| `DB_USER`        | Yes      | Database user                                  |
| `DB_PASSWORD`    | Yes      | Database password                              |
| `JWT_SECRET`     | Yes      | Secret for signing JWTs                        |
| `JWT_EXPIRES_IN` | No       | JWT expiry (default: 7d)                       |
| `FRONTEND_URL`   | Yes      | Allowed frontend origin for CORS and Socket.IO |

---

## API Overview

| Resource  | Base Path        |
| --------- | ---------------- |
| Auth      | `/api/auth`      |
| Projects  | `/api/projects`  |
| API Keys  | `/api/api-keys`  |
| Telemetry | `/api/telemetry` |
| Requests  | `/api/requests`  |
| Analytics | `/api/analytics` |
| Errors    | `/api/errors`    |
| Endpoints | `/api/endpoints` |

---

## Telemetry

Connected Express applications send request telemetry to RouteHound using a project-specific API key.

Each telemetry record can include:

| Field         | Description                            |
| ------------- | -------------------------------------- |
| Method        | HTTP request method                    |
| Endpoint      | Requested API route                    |
| Status Code   | HTTP response status code              |
| Response Time | Request duration in milliseconds       |
| Error         | Captured error information, if present |
| Timestamp     | Time the request was completed         |

---

## Analytics

RouteHound processes stored request telemetry to provide:

* Total request volume
* Successful and failed request counts
* Error rate
* Average response time
* Request volume over time
* Endpoint-level request counts
* Endpoint-level error rates
* Endpoint-level response times
* p50 latency
* p95 latency

---

## Real-Time Monitoring

Socket.IO is used to push new request telemetry to connected frontend clients as it arrives.

Live events are isolated by project so dashboards only receive telemetry for the currently selected application.

---

## Frontend

This backend connects to the [RouteHound Frontend](https://github.com/snageshprasad/route-hound-frontend).

---

## License

Copyright (c) 2026 Nagesh Prasad Sahoo. All Rights Reserved.

This source code is publicly visible for portfolio and review purposes only.
Unauthorized use, copying, modification, distribution, or commercial use
of this code without explicit written permission from the author is strictly prohibited.
