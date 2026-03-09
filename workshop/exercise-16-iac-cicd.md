# Exercise 16 — Infrastructure as Code & CI/CD Pipelines

**Duration**: 4 minutes  
**Copilot Feature**: DevOps Custom Agent + Prompt Files  
**Goal**: Generate Docker, Terraform/Bicep, and GitHub Actions pipelines for the ITMS application.

---

## Step 1 — Switch to the DevOps Agent

In Copilot Chat, select **DevOps & IaC Agent** from the agent dropdown.

---

## Step 2 — Create Docker Configuration

```
Read doc/tsd.md (Infrastructure & Deployment section) and src/.

Create:
1. infra/docker/Dockerfile — multi-stage build (builder + minimal runtime), non-root user, HEALTHCHECK using /api/v1/health
2. infra/docker/docker-compose.yml — services: api, db (PostgreSQL), redis; mount db/migrations/ for auto-migration; .env for variables; health check depends_on
3. .dockerignore — exclude: node_modules, .env, .git, tests/, coverage/, *.log, doc/

Build the Docker image and confirm it succeeds.
```

---

## Step 3 — Create Infrastructure as Code (Azure)

```
Create Azure Bicep templates in infra/bicep/:

1. main.bicep — entry point deploying all modules
2. modules/container-app.bicep — Azure Container App for the API
3. modules/database.bicep — Azure Database for PostgreSQL (Flexible Server)
4. modules/keyvault.bicep — Azure Key Vault for secrets (DB password, JWT secret, SendGrid key)
5. modules/container-registry.bicep — Azure Container Registry
6. modules/monitoring.bicep — Application Insights + Log Analytics
7. parameters/dev.json and parameters/prod.json

Security requirements:
- Container App uses managed identity to access Key Vault (no secrets in env vars)
- PostgreSQL only accessible within VNet (no public endpoint)
- All resources tagged: environment, project=ITMS, owner
```

> **Prefer Terraform?** Replace "Bicep" with "Terraform" in the prompt above.

---

## Step 4 — Create CI/CD Pipelines

```
Create GitHub Actions workflows in .github/workflows/:

1. ci.yml (triggers: PR to main):
   - Checkout, setup runtime (cache deps), install, lint (fail on warnings)
   - Unit tests (fail if coverage < 80%)
   - Build Docker image
   - Trivy container security scan (fail on CRITICAL)
   - Semgrep static analysis (fail on HIGH)
   - Comment results on PR

2. cd-staging.yml (triggers: push to main):
   - Build + push Docker image to ACR (tag: main-{commit-sha})
   - Run database migrations against staging DB
   - Deploy to Azure Container App (staging) using GitHub OIDC
   - Smoke test: GET /api/v1/health must return 200
   - Notify Teams channel on success/failure

3. cd-production.yml (triggers: push tag v*.*.*):
   - Manual approval gate (environment: production)
   - Build + push Docker image (tag: {version})
   - Blue-green deploy with gradual traffic shift
   - Health check: poll /api/v1/health for 2 minutes
   - Automatic rollback on failure
   - Create GitHub Release with changelog

Use GitHub OIDC for Azure authentication. Store secrets in GitHub Environments.
```

---

## Verify

- [ ] Docker image builds successfully
- [ ] `ci.yml` workflow has linting, test, build, and security scanning steps
- [ ] `cd-staging.yml` deploys via OIDC (no stored secrets)
- [ ] `cd-production.yml` has manual approval and rollback steps

---

> **⚡ Extension**: `Create infra/README.md with deployment prerequisites, first-time setup steps, day-to-day release guide, rollback instructions, and cost estimation for 500 concurrent users.`

---

## Workshop Complete!

Congratulations — you have taken the ITMS project from raw requirement through the full SDLC:

| Exercise | Output |
|----------|--------|
| 01-04 | doc/brd.md, doc/tsd.md, doc/frd.md |
| 05 | .github/copilot-instructions.md |
| 06-07 | doc/implementation-plan.md, .github/prompts/ |
| 08 | GitHub Issues + Milestones |
| 09-12 | Working REST API + Database layer |
| 13 | Test suite with ≥ 80% coverage |
| 14 | Security-hardened codebase + report |
| 15 | Passing build + end-to-end flow |
| 16 | Docker + IaC + CI/CD pipelines |
