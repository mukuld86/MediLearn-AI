# MediLearn AI

MediLearn AI is an AI-driven study platform for medical learners. It creates personalized quizzes, delivers intelligent feedback, and tracks progress while demonstrating a full-stack deployment and monitoring pipeline.

---

## Overview

MediLearn AI combines:

* adaptive quiz generation
* AI-assisted grading and learning feedback
* secure user sessions and persistent progress tracking
* a production-ready deployment workflow with observability

It is designed as both a learning product and a technical showcase.

---

## Key Features

* Personalized quiz creation by topic and context
* AI-powered answer evaluation and feedback
* User profiles, progress tracking, and leaderboard
* Secure authentication with HttpOnly session cookies
* Persistent storage using MongoDB Atlas
* Prometheus metrics and Grafana dashboards for monitoring

---

## Architecture

```text
User → Next.js app → Node backend
     ↓              ↓
  Authentication   MongoDB
                   Metrics → Prometheus → Grafana
```

---

## Tech Stack

* Next.js (App Router)
* TypeScript
* React + Tailwind CSS
* Shadcn/UI components
* Node.js backend server
* MongoDB Atlas
* Google Gemini via Genkit
* Docker and Kubernetes for deployment
* Prometheus + Grafana for observability

---

## Local Setup

### Prerequisites

* Node.js 18+
* npm
* MongoDB Atlas cluster

### Install

```bash
npm install
```

### Environment

Create `.env.local` with values similar to:

```env
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
MONGODB_URI=mongodb+srv://<user>:<password>@<cluster-url>/medilearn?retryWrites=true&w=majority
MONGODB_DB_NAME=medilearn
AUTH_JWT_SECRET=YOUR_LONG_RANDOM_SECRET
```

### Start the app

```bash
npm run dev
```

Then open:

```text
http://localhost:3000
```

---

## Docker

Build and run the container:

```bash
docker build -t medilearn-ai .
docker run -p 3000:3000 medilearn-ai
```

---

## Kubernetes Deployment

This repository includes Kubernetes manifests for deployment.

```bash
minikube start
eval $(minikube docker-env)

docker build -t medilearn-ai .

kubectl apply -f aws-deployment.yaml
kubectl apply -f aws-service.yaml
kubectl apply -f aws-servicemonitor.yaml
```

To access the service:

```bash
minikube service medilearn-service
```

---

## Monitoring and Observability

### Prometheus

* Scrape the metrics endpoint at:

```text
http://<service-address>/api/metrics
```

### Grafana

* Add Prometheus as a data source
* Build dashboards with application metrics

### Metrics exposed

* `app_requests_total`
* `app_latency_ms`
* `app_errors_total`
* `app_success_total`
* `app_active_users`
* `app_db_query_time_ms`
* `app_uptime_seconds`

---

## Project Structure

* `src/app` — application pages and API routes
* `src/lib` — utilities, database, and auth helpers
* `src/components` — reusable UI components
* `server.js` — server entry point
* `Dockerfile` — container build definition
* `aws-deployment.yaml`, `aws-service.yaml`, `aws-servicemonitor.yaml` — deployment manifests

---

## Future Improvements

* Add P95/P99 latency tracking
* Implement alerting with Grafana Alertmanager
* Add endpoint-level metrics
* Deploy on AWS EKS/ECS
* Integrate Redis caching
* Harden security and authentication

---

## Author

Mukul Deshwal

GitHub: https://github.com/mukuld86

