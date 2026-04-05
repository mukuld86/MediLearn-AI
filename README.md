# MediLearn AI

MediLearn AI is an AI-powered study platform for medical students and professionals. It generates personalized quizzes, provides intelligent feedback, and tracks learning progress to enhance understanding and retention.

Beyond core functionality, this project demonstrates a **complete DevOps-driven deployment and observability pipeline**, making it a full-stack + infrastructure showcase.

---

##  Core Features

*  Personalized quiz generation by topic and context
*  AI-powered grading and feedback
*  User profiles and leaderboard
*  Email/password authentication with secure HttpOnly session cookies
*  MongoDB Atlas-backed persistence for users and quiz results
*  Real-time application monitoring using Prometheus & Grafana

---

## Tech Stack

### Application Layer

* **Framework:** Next.js (App Router)
* **Language:** TypeScript
* **AI:** Google Gemini via Genkit
* **UI:** React, Shadcn/UI, Tailwind CSS
* **Backend:** Custom Node.js server (`server.js`)
* **Database:** MongoDB Atlas

---

### DevOps & Infrastructure

This project includes a **complete DevOps workflow**:

#### Containerization

* Dockerized the application using a production-ready Dockerfile
* Built optimized images for deployment

#### Kubernetes (Minikube)

* Deployed using **Deployment + Service (NodePort)**
* Managed pods and container lifecycle
* Enabled scalable and isolated environment

#### Monitoring & Observability

Implemented **application-level monitoring** (not just infrastructure):

* Custom `/api/metrics` endpoint (Prometheus format)
* Prometheus configured to scrape application metrics
* Grafana dashboards built for real-time visualization

###  Metrics Monitored

* `app_requests_total` → Traffic
* `app_latency_ms` → Performance
* `app_errors_total` → Reliability
* `app_success_total` → Success rate
* `app_active_users` → User activity
* `app_db_query_time_ms` → Database performance
* `app_uptime_seconds` → Stability

---

##  Architecture

```text
User → Kubernetes Service → App (Next.js + Node)
     → /api/metrics → Prometheus → Grafana Dashboard
```

---

##  Getting Started

### 🔹 Prerequisites

* Node.js 18+
* npm
* MongoDB Atlas cluster

---

### 🔹 Installation

1. Install dependencies:

```bash
npm install
```

2. Create `.env.local`:

```env
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/medilearn?retryWrites=true&w=majority
MONGODB_DB_NAME=medilearn
AUTH_JWT_SECRET=YOUR_LONG_RANDOM_SECRET
```

3. Run the app:

```bash
npm run dev
```

Open: http://localhost:3000

---

## 🐳 Docker Setup

```bash
docker build -t medilearn-ai .
docker run -p 3000:3000 medilearn-ai
```

---

## Kubernetes Deployment (Minikube)

```bash
minikube start
eval $(minikube docker-env)

docker build -t medilearn-ai .

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

minikube service medilearn-service
```

---

##  Monitoring Setup

### Prometheus

* Configure scrape target:

  ```
  medilearn-service:3000/api/metrics
  ```

### Grafana

* Add Prometheus as data source
* Create dashboards using PromQL queries

---

##  Dashboard Highlights

The Grafana dashboard includes:

*  Requests per second
*  Latency trends
*  Active users
*  Error rate
*  Success rate
*  Database performance
*  Uptime

---

## Future Scope

*  Add latency histograms (P95 / P99 monitoring)
*  Implement alerting (Grafana / Alertmanager)
*  Per-API endpoint metrics
*  Replace simulated metrics with real production tracking
*  Deploy on AWS (EKS / ECS)
*  Add caching layer (Redis)
*  Improve authentication and security mechanisms

---

## Notes

* Authentication APIs: `src/app/api/auth`
* Leaderboard API: `src/app/api/leaderboard`
* Quiz API: `src/app/api/quiz/complete`
* Metrics endpoint: `src/app/api/metrics`

---

## Author

**Mukul Deshwal**:
 GitHub: https://github.com/mukuld86

---

## Conclusion

MediLearn AI is not just an AI-based learning platform—it is a **complete end-to-end system** that demonstrates:

* Scalable deployment using Kubernetes
* Containerization using Docker
* Real-time monitoring with Prometheus
* Data visualization with Grafana

This project highlights how modern applications can be built, deployed, and monitored using **industry-standard DevOps practices**, making it both a functional product and a strong engineering showcase.

---
