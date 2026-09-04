# CineBook Telugu

Three-tier Telugu movie-ticket platform: React/Nginx frontend, Spring Boot API, PostgreSQL database, login, booking/payment records, and Helm + Argo CD deployment.

## Local run
```bash
cp .env.example .env
docker compose up --build
```
Open `http://localhost:8080`; demo account: `demo@cinebook.local` / `Demo@123`.

Payment is a safe demo checkout: it records a payment reference and never receives card/CVV data. Use Razorpay/Stripe before production. Set Twilio SMS credentials as Kubernetes secrets for real SMS; never commit them.

## Kubernetes / GitOps
Build and push the two images to ECR, update `helm/cinebook/values-prod.yaml`, create `cinebook-secrets` from `k8s/secret.example.yaml` (prefer AWS Secrets Manager + External Secrets), then apply `argocd/application.yaml`.
