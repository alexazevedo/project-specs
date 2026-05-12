# GoRank 30-Day MVP Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a shippable GoRank MVP that can onboard a Brazilian brand, generate pt-BR prompts, run AI visibility monitoring, extract mentions/citations, audit the website, generate prioritized recommendations, produce a client report, and support a managed-service pilot.

**Architecture:** Monorepo with a Next.js dashboard, FastAPI backend, PostgreSQL, Redis, Temporal workflows, and provider-agnostic AI/search adapters. The MVP is evidence-first: store raw prompt answers, audit findings, extracted mentions/citations, recommendation rationale, and report snapshots.

**Tech Stack:** Next.js, React, TypeScript, Tailwind, shadcn/ui, Python, FastAPI, PostgreSQL, Redis, Temporal, SQLAlchemy/Alembic, pgvector, Docker Compose, Playwright, pytest.

---

## Scope

This plan implements the first vertical slice:

1. Brand onboarding.
2. Prompt generation and approval.
3. Monitoring runs for a limited set of compliant engines/providers.
4. Mention, competitor, citation, sentiment, and position extraction.
5. Site/GEO audit.
6. Recommendation generation.
7. HTML/PDF report.
8. Free checker.
9. Managed-service admin workflow.
10. Reviewable remediation artifact generation.

Not in MVP:

- Auto-publishing.
- Auto-merging PRs.
- Enterprise SSO.
- Full billing.
- Unsupported browser automation.
- Real-time monitoring at scale.

## Repository Layout

Create this structure:

```text
gorank/
  apps/
    web/
      app/
      components/
      lib/
      tests/
    api/
      app/
        api/
        core/
        db/
        models/
        schemas/
        services/
        workflows/
        agents/
        integrations/
        reports/
      tests/
  packages/
    shared/
      types/
  infra/
    docker/
    temporal/
  docs/
    product/
    operations/
  .env.example
  docker-compose.yml
  README.md
```

## File Responsibilities

- `apps/api/app/main.py`: FastAPI app bootstrap.
- `apps/api/app/core/config.py`: environment settings.
- `apps/api/app/db/session.py`: SQLAlchemy session management.
- `apps/api/app/models/*.py`: database models.
- `apps/api/app/schemas/*.py`: Pydantic request/response schemas.
- `apps/api/app/api/routes_*.py`: API routers by domain.
- `apps/api/app/services/*`: business logic.
- `apps/api/app/workflows/*`: Temporal workflows and activities.
- `apps/api/app/agents/*`: structured LLM/extraction/recommendation agents.
- `apps/api/app/integrations/*`: provider adapters for LLM/search/GitHub/CMS.
- `apps/api/app/reports/*`: report rendering.
- `apps/web/app/*`: Next.js routes.
- `apps/web/components/*`: reusable UI.
- `packages/shared/types/*`: shared API and domain types.

## Data Model Implementation Order

1. Identity/tenant tables: users, organizations, memberships, workspaces.
2. Brand tables: brands, competitors.
3. Prompt/monitoring tables: ai_engines, prompts, prompt_runs, answers.
4. Extraction tables: mentions, sources, citations.
5. Scoring/audit tables: visibility_scores, audits, audit_findings.
6. Action tables: recommendations, executions, reports, alerts, tasks.
7. Integration/cost tables: github_integrations, cms_integrations, subscriptions, usage_costs.

## Week 1: Foundation and Onboarding

### Task 1: Bootstrap Monorepo

**Files:**

- Create: `package.json`
- Create: `apps/web/package.json`
- Create: `apps/api/pyproject.toml`
- Create: `docker-compose.yml`
- Create: `.env.example`
- Create: `README.md`

- [ ] **Step 1: Initialize repository structure**

Run:

```bash
mkdir -p apps/web apps/api/app packages/shared/types infra/docker infra/temporal docs/product docs/operations
```

Expected: folders exist.

- [ ] **Step 2: Add Docker Compose services**

Create `docker-compose.yml` with:

```yaml
services:
  postgres:
    image: pgvector/pgvector:pg16
    environment:
      POSTGRES_USER: gorank
      POSTGRES_PASSWORD: gorank
      POSTGRES_DB: gorank
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7
    ports:
      - "6379:6379"

  temporal:
    image: temporalio/auto-setup:1.25
    environment:
      DB: postgresql
      DB_PORT: 5432
      POSTGRES_USER: gorank
      POSTGRES_PWD: gorank
      POSTGRES_SEEDS: postgres
    depends_on:
      - postgres
    ports:
      - "7233:7233"

volumes:
  postgres_data:
```

- [ ] **Step 3: Add environment template**

Create `.env.example` with:

```dotenv
DATABASE_URL=postgresql+psycopg://gorank:gorank@localhost:5432/gorank
REDIS_URL=redis://localhost:6379/0
TEMPORAL_ADDRESS=localhost:7233
APP_ENV=development
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
GOOGLE_API_KEY=
PERPLEXITY_API_KEY=
SERP_API_KEY=
GITHUB_APP_ID=
GITHUB_PRIVATE_KEY=
```

- [ ] **Step 4: Verify services**

Run:

```bash
docker compose up -d postgres redis temporal
docker compose ps
```

Expected: postgres, redis, temporal are running.

- [ ] **Step 5: Commit**

Run:

```bash
git add package.json apps/web apps/api docker-compose.yml .env.example README.md
git commit -m "chore: bootstrap gorank monorepo"
```

If the workspace is not yet a git repo, initialize it first with `git init`.

### Task 2: FastAPI Foundation

**Files:**

- Create: `apps/api/app/main.py`
- Create: `apps/api/app/core/config.py`
- Create: `apps/api/app/db/session.py`
- Create: `apps/api/app/api/router.py`
- Create: `apps/api/tests/test_health.py`

- [ ] **Step 1: Add health test**

Create `apps/api/tests/test_health.py`:

```python
from fastapi.testclient import TestClient

from app.main import app


def test_health_returns_ok():
    client = TestClient(app)
    response = client.get("/health")
    assert response.status_code == 200
    assert response.json() == {"status": "ok"}
```

- [ ] **Step 2: Verify failing test**

Run:

```bash
cd apps/api
pytest tests/test_health.py -v
```

Expected: fail because `app.main` does not exist.

- [ ] **Step 3: Implement app**

Create `apps/api/app/main.py`:

```python
from fastapi import FastAPI

app = FastAPI(title="GoRank API", version="0.1.0")


@app.get("/health")
def health() -> dict[str, str]:
    return {"status": "ok"}
```

- [ ] **Step 4: Verify passing test**

Run:

```bash
cd apps/api
pytest tests/test_health.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: add api health endpoint"
```

### Task 3: Database Models and Migrations

**Files:**

- Create: `apps/api/app/models/base.py`
- Create: `apps/api/app/models/tenant.py`
- Create: `apps/api/app/models/brand.py`
- Create: `apps/api/app/models/monitoring.py`
- Create: `apps/api/app/models/audit.py`
- Create: `apps/api/app/models/action.py`
- Create: `apps/api/alembic/env.py`
- Create: `apps/api/tests/test_models.py`

- [ ] **Step 1: Write model relationship test**

Create `apps/api/tests/test_models.py`:

```python
from app.models.brand import Brand, Competitor
from app.models.tenant import Organization, Workspace


def test_brand_competitor_relationships_are_declared():
    assert Organization.__tablename__ == "organizations"
    assert Workspace.__tablename__ == "workspaces"
    assert Brand.__tablename__ == "brands"
    assert Competitor.__tablename__ == "competitors"
```

- [ ] **Step 2: Verify failing test**

Run:

```bash
cd apps/api
pytest tests/test_models.py -v
```

Expected: fail because models do not exist.

- [ ] **Step 3: Implement core models**

Implement the tables from the product blueprint using SQLAlchemy 2.0 typed models. Keep models split by responsibility:

- `tenant.py`: `User`, `Organization`, `OrganizationMember`, `Workspace`.
- `brand.py`: `Brand`, `Competitor`.
- `monitoring.py`: `AIEngine`, `Prompt`, `PromptRun`, `Answer`, `Mention`, `Source`, `Citation`, `VisibilityScore`.
- `audit.py`: `Audit`, `AuditFinding`.
- `action.py`: `Recommendation`, `Execution`, `Report`, `Alert`, `Task`, `Subscription`, `UsageCost`, `GitHubIntegration`, `CMSIntegration`.

- [ ] **Step 4: Verify passing test**

Run:

```bash
cd apps/api
pytest tests/test_models.py -v
```

Expected: pass.

- [ ] **Step 5: Generate migration**

Run:

```bash
cd apps/api
alembic revision --autogenerate -m "create initial schema"
alembic upgrade head
```

Expected: tables created in local PostgreSQL.

- [ ] **Step 6: Commit**

```bash
git add apps/api
git commit -m "feat: add initial database schema"
```

### Task 4: Brand Onboarding API

**Files:**

- Create: `apps/api/app/schemas/brand.py`
- Create: `apps/api/app/services/brands.py`
- Create: `apps/api/app/api/routes_brands.py`
- Modify: `apps/api/app/main.py`
- Test: `apps/api/tests/test_brand_routes.py`

- [ ] **Step 1: Write failing route test**

Create `apps/api/tests/test_brand_routes.py` with a test that posts a workspace brand and expects persisted fields:

```python
def test_create_brand(client, db_session):
    response = client.post(
        "/api/v1/workspaces/test-workspace/brands",
        json={
            "name": "Silva Advocacia",
            "domain": "https://silva.example",
            "category": "advocacia trabalhista",
            "industry": "legal",
            "country": "BR",
            "language": "pt-BR",
            "target_locations": [{"city": "Sao Paulo", "state": "SP"}],
            "competitors": [{"name": "Concorrente Legal", "domain": "https://concorrente.example"}],
            "business_goals": ["gerar leads qualificados"],
            "conversion_goals": ["agendar consulta"],
        },
    )
    assert response.status_code == 201
    body = response.json()
    assert body["name"] == "Silva Advocacia"
    assert body["language"] == "pt-BR"
```

- [ ] **Step 2: Implement schemas and service**

Add Pydantic schemas for `BrandCreate`, `BrandRead`, `CompetitorCreate`, and `CompetitorRead`. Implement service methods:

- `create_brand(workspace_id, payload)`.
- `get_brand(brand_id)`.
- `update_brand(brand_id, payload)`.
- `list_competitors(brand_id)`.

- [ ] **Step 3: Implement routes**

Add:

- `POST /api/v1/workspaces/{workspace_id}/brands`
- `GET /api/v1/brands/{brand_id}`
- `PATCH /api/v1/brands/{brand_id}`
- `GET /api/v1/brands/{brand_id}/competitors`

- [ ] **Step 4: Run tests**

Run:

```bash
cd apps/api
pytest tests/test_brand_routes.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: add brand onboarding api"
```

## Week 2: Prompt Monitoring and Metrics

### Task 5: Prompt Generation Service

**Files:**

- Create: `apps/api/app/services/prompt_templates.py`
- Create: `apps/api/app/services/prompts.py`
- Create: `apps/api/app/api/routes_prompts.py`
- Test: `apps/api/tests/test_prompt_generation.py`

- [ ] **Step 1: Write failing prompt generation test**

Expected behavior: for a legal brand in Sao Paulo, generate at least 30 prompts across commercial, local, comparison, alternatives, informational, and branded fact-check intents.

- [ ] **Step 2: Implement pt-BR templates**

Create templates such as:

```python
PT_BR_PROMPT_TEMPLATES = [
    ("local", "Qual melhor {category} em {city}?"),
    ("commercial", "Qual empresa contratar para {service} em {city}?"),
    ("comparison", "{brand} ou {competitor}: qual escolher para {service}?"),
    ("alternatives", "Alternativas ao {competitor} no Brasil"),
    ("problem_solution", "Como resolver {problem} com uma empresa especializada?"),
    ("branded_fact", "O que e a {brand} e quais servicos oferece?"),
]
```

- [ ] **Step 3: Add API routes**

Add:

- `POST /api/v1/brands/{brand_id}/prompts/generate`
- `GET /api/v1/brands/{brand_id}/prompts`
- `PATCH /api/v1/prompts/{prompt_id}`
- `POST /api/v1/prompts/bulk-approve`

- [ ] **Step 4: Run tests**

Run:

```bash
cd apps/api
pytest tests/test_prompt_generation.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: generate portuguese ai visibility prompts"
```

### Task 6: Provider Adapter Interface

**Files:**

- Create: `apps/api/app/integrations/ai/base.py`
- Create: `apps/api/app/integrations/ai/openai_adapter.py`
- Create: `apps/api/app/integrations/ai/perplexity_adapter.py`
- Create: `apps/api/app/integrations/search/serp_adapter.py`
- Test: `apps/api/tests/test_provider_adapters.py`

- [ ] **Step 1: Write adapter contract test**

The contract should require:

- `engine_slug`.
- `run_prompt(prompt, region, language)`.
- return `ProviderAnswer(raw_text, citations, metadata, cost_usd)`.

- [ ] **Step 2: Implement base dataclasses/protocol**

Use Python `Protocol` and dataclasses. Keep provider output normalized.

- [ ] **Step 3: Implement adapters with test doubles**

For MVP tests, provider adapters should support a fake mode that returns deterministic answers without network calls.

- [ ] **Step 4: Run tests**

Run:

```bash
cd apps/api
pytest tests/test_provider_adapters.py -v
```

Expected: pass without API keys.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: add ai provider adapter contracts"
```

### Task 7: Monitoring Workflow

**Files:**

- Create: `apps/api/app/workflows/monitoring.py`
- Create: `apps/api/app/services/monitoring.py`
- Create: `apps/api/app/api/routes_monitoring.py`
- Test: `apps/api/tests/test_monitoring_workflow.py`

- [ ] **Step 1: Write failing workflow test**

Expected: approved prompts create prompt runs, answers, cost records, and completed status.

- [ ] **Step 2: Implement monitoring service**

Implement:

- `create_monitoring_run(brand_id, prompt_ids, engine_ids)`.
- `run_prompt_once(prompt_id, engine_id)`.
- `store_answer(prompt_run_id, provider_answer)`.

- [ ] **Step 3: Implement API routes**

Add:

- `POST /api/v1/brands/{brand_id}/monitoring/runs`
- `GET /api/v1/brands/{brand_id}/monitoring/runs`
- `GET /api/v1/prompt-runs/{run_id}`

- [ ] **Step 4: Run tests**

Run:

```bash
cd apps/api
pytest tests/test_monitoring_workflow.py -v
```

Expected: pass with fake provider.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: run prompt monitoring workflow"
```

### Task 8: Extraction Agents

**Files:**

- Create: `apps/api/app/agents/extraction.py`
- Create: `apps/api/app/services/extraction.py`
- Test: `apps/api/tests/test_extraction.py`

- [ ] **Step 1: Write extraction tests**

Test input:

```text
Para automacao de WhatsApp no Brasil, empresas como Zenvia, Take Blip e GoRank podem ser consideradas. A GoRank e mais focada em visibilidade em IA. Fontes: https://example.com/gorank, https://competitor.example/whatsapp
```

Expected:

- GoRank mention found.
- Competitor mentions found.
- Source URLs extracted.
- Position order assigned.
- Sentiment is neutral/positive.

- [ ] **Step 2: Implement deterministic extraction first**

Use string/entity matching and URL parsing before LLM extraction.

- [ ] **Step 3: Add optional LLM structured extraction**

Use structured JSON output only when deterministic extraction is insufficient.

- [ ] **Step 4: Run tests**

Run:

```bash
cd apps/api
pytest tests/test_extraction.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: extract mentions and citations"
```

### Task 9: Visibility Scores

**Files:**

- Create: `apps/api/app/services/scoring.py`
- Create: `apps/api/app/api/routes_scores.py`
- Test: `apps/api/tests/test_scoring.py`

- [ ] **Step 1: Write scoring test**

Given 10 prompts, 4 brand mentions, 6 competitor mentions, average position 2.2, and citation share 0.3, score should return component values and a bounded 0-100 composite.

- [ ] **Step 2: Implement transparent formula**

Use:

```python
score = (
    mention_rate * 0.30
    + recommendation_share * 0.25
    + citation_share * 0.20
    + position_score * 0.15
    + sentiment_score * 0.10
) * 100
```

Store component scores with the composite.

- [ ] **Step 3: Add API route**

Add:

- `GET /api/v1/brands/{brand_id}/scores`

- [ ] **Step 4: Run tests**

```bash
cd apps/api
pytest tests/test_scoring.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: calculate ai visibility scores"
```

## Week 3: Audit, Recommendations, Reports, Free Checker

### Task 10: Site Audit Crawler

**Files:**

- Create: `apps/api/app/services/crawler.py`
- Create: `apps/api/app/services/audits.py`
- Create: `apps/api/app/api/routes_audits.py`
- Test: `apps/api/tests/test_site_audit.py`

- [ ] **Step 1: Write audit tests**

Test a local HTML fixture with missing Organization schema, missing sitemap, weak H1, and no FAQ section. Expected findings should include severity and affected URL.

- [ ] **Step 2: Implement crawler**

Features:

- Fetch robots.txt.
- Fetch sitemap.xml.
- Crawl up to configured page limit.
- Extract title, description, canonical, headings, links, JSON-LD, visible text.
- Respect timeout and rate limits.

- [ ] **Step 3: Implement audit checks**

Checks:

- robots/sitemap availability.
- Organization/LocalBusiness schema.
- canonical.
- title/meta description.
- headings.
- textual content length.
- FAQ/comparison/local page existence.
- internal link count.

- [ ] **Step 4: Run tests**

```bash
cd apps/api
pytest tests/test_site_audit.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: add site geo audit"
```

### Task 11: Recommendation Engine

**Files:**

- Create: `apps/api/app/agents/recommendations.py`
- Create: `apps/api/app/services/recommendations.py`
- Create: `apps/api/app/api/routes_recommendations.py`
- Test: `apps/api/tests/test_recommendations.py`

- [ ] **Step 1: Write recommendation test**

Given:

- brand missing from local prompts.
- competitor cited from directory.
- site missing LocalBusiness schema.

Expected:

- recommendation title: "Add LocalBusiness schema to key service pages".
- type: `schema`.
- confidence above 0.7.
- approval required true.
- success metric references local prompt retest.

- [ ] **Step 2: Implement recommendation schema**

Fields must match product blueprint:

- title, type, affected URL/file, reason, evidence, expected impact, confidence, effort, priority score, implementation steps, risk, auto-executable, approval required, success metric, re-test plan.

- [ ] **Step 3: Implement priority scoring**

Use:

```python
priority_score = (impact * confidence * prompt_value * competitor_gap) / max(effort, 1)
```

- [ ] **Step 4: Add API routes**

Add:

- `POST /api/v1/brands/{brand_id}/recommendations/generate`
- `GET /api/v1/brands/{brand_id}/recommendations`
- `POST /api/v1/recommendations/{recommendation_id}/approve`
- `POST /api/v1/recommendations/{recommendation_id}/reject`

- [ ] **Step 5: Run tests**

```bash
cd apps/api
pytest tests/test_recommendations.py -v
```

Expected: pass.

- [ ] **Step 6: Commit**

```bash
git add apps/api
git commit -m "feat: generate prioritized geo recommendations"
```

### Task 12: Report Renderer

**Files:**

- Create: `apps/api/app/reports/templates/visibility_report.html`
- Create: `apps/api/app/reports/render.py`
- Create: `apps/api/app/services/reports.py`
- Create: `apps/api/app/api/routes_reports.py`
- Test: `apps/api/tests/test_reports.py`

- [ ] **Step 1: Write report test**

Expected report HTML includes:

- Executive summary.
- Visibility score.
- Competitor comparison.
- Top lost prompts.
- Citation analysis.
- Technical audit findings.
- Recommendations.
- Next action plan.

- [ ] **Step 2: Implement HTML renderer**

Use Jinja2. Keep styling print-friendly and PDF-ready.

- [ ] **Step 3: Implement API routes**

Add:

- `POST /api/v1/brands/{brand_id}/reports`
- `GET /api/v1/brands/{brand_id}/reports`
- `GET /api/v1/reports/{report_id}`

- [ ] **Step 4: Run tests**

```bash
cd apps/api
pytest tests/test_reports.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: render ai visibility reports"
```

### Task 13: Free Checker

**Files:**

- Create: `apps/api/app/services/free_checker.py`
- Create: `apps/api/app/api/routes_free_checker.py`
- Create: `apps/web/app/(marketing)/free-checker/page.tsx`
- Test: `apps/api/tests/test_free_checker.py`

- [ ] **Step 1: Write free checker test**

Expected: posting brand, website, category, competitors, country/city, and email creates a limited run and returns a mini-report ID.

- [ ] **Step 2: Implement lead capture and quota**

Rules:

- Max 1 active free checker run per email/domain per day.
- Max 10 prompts.
- Mark outputs as sample-only.

- [ ] **Step 3: Implement public form**

Fields:

- brand, website, category, competitors, country/city, email.

Copy:

```text
Sua marca aparece quando alguem pergunta no ChatGPT?
Receba uma amostra gratis da sua visibilidade em respostas de IA.
```

- [ ] **Step 4: Run tests**

```bash
cd apps/api
pytest tests/test_free_checker.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api apps/web
git commit -m "feat: add free ai visibility checker"
```

## Week 4: Dashboard, Execution Artifacts, Pilot Hardening

### Task 14: Dashboard Shell

**Files:**

- Create: `apps/web/app/(app)/layout.tsx`
- Create: `apps/web/app/(app)/workspaces/page.tsx`
- Create: `apps/web/app/(app)/brands/[brandId]/page.tsx`
- Create: `apps/web/components/nav/sidebar.tsx`
- Create: `apps/web/components/metrics/visibility-score-card.tsx`
- Test: `apps/web/tests/dashboard.spec.ts`

- [ ] **Step 1: Write Playwright smoke test**

Expected: dashboard renders sidebar, score card, prompt table link, recommendations link, reports link.

- [ ] **Step 2: Implement dashboard layout**

Navigation items:

- Overview.
- Prompts.
- Monitoring.
- Competitors.
- Sources.
- Audit.
- Recommendations.
- Reports.
- Alerts.
- Integrations.

- [ ] **Step 3: Implement overview cards**

Cards:

- AI Visibility Score.
- Share of Mentions.
- Average Position.
- Citation Share.
- Top Competitor.
- Open Recommendations.

- [ ] **Step 4: Run frontend test**

```bash
cd apps/web
npm run test:e2e
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/web
git commit -m "feat: add dashboard shell"
```

### Task 15: Prompt and Monitoring UI

**Files:**

- Create: `apps/web/app/(app)/brands/[brandId]/prompts/page.tsx`
- Create: `apps/web/app/(app)/brands/[brandId]/monitoring/page.tsx`
- Create: `apps/web/components/prompts/prompt-table.tsx`
- Create: `apps/web/components/monitoring/answer-evidence-panel.tsx`

- [ ] **Step 1: Add prompt table**

Columns:

- prompt text, intent, persona, location, priority, status, last run, actions.

- [ ] **Step 2: Add monitoring table**

Columns:

- prompt, engine, brand mentioned, competitors, position, citations, sentiment, timestamp.

- [ ] **Step 3: Add answer evidence drawer**

Show raw answer, citations, extraction details, and run metadata.

- [ ] **Step 4: Run UI smoke tests**

```bash
cd apps/web
npm run test:e2e
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/web
git commit -m "feat: add prompt and monitoring ui"
```

### Task 16: Recommendations and Reports UI

**Files:**

- Create: `apps/web/app/(app)/brands/[brandId]/recommendations/page.tsx`
- Create: `apps/web/app/(app)/brands/[brandId]/reports/page.tsx`
- Create: `apps/web/components/recommendations/recommendation-card.tsx`
- Create: `apps/web/components/reports/report-preview.tsx`

- [ ] **Step 1: Add recommendation action center**

Each recommendation displays:

- type, reason, evidence, impact, confidence, effort, risk, approval controls.

- [ ] **Step 2: Add report list and preview**

Actions:

- generate report.
- open report.
- download/print PDF.

- [ ] **Step 3: Run UI smoke tests**

```bash
cd apps/web
npm run test:e2e
```

Expected: pass.

- [ ] **Step 4: Commit**

```bash
git add apps/web
git commit -m "feat: add recommendation and report ui"
```

### Task 17: Execution Artifact Generator

**Files:**

- Create: `apps/api/app/services/executions.py`
- Create: `apps/api/app/integrations/github/patch_generator.py`
- Create: `apps/api/app/integrations/cms/markdown_export.py`
- Create: `apps/api/app/api/routes_executions.py`
- Test: `apps/api/tests/test_executions.py`

- [ ] **Step 1: Write execution tests**

Given an approved schema recommendation, expected artifact:

- JSON-LD snippet.
- implementation steps.
- PR description with GEO rationale.
- approval required.

- [ ] **Step 2: Implement Markdown export**

Generate:

- content brief.
- FAQ draft.
- schema snippet.
- local page draft.
- comparison page outline.

- [ ] **Step 3: Implement GitHub patch prototype**

MVP output can be a downloadable patch file even before GitHub App review.

- [ ] **Step 4: Add execution routes**

Add:

- `POST /api/v1/recommendations/{recommendation_id}/executions`
- `GET /api/v1/executions/{execution_id}`
- `POST /api/v1/executions/{execution_id}/mark-complete`

- [ ] **Step 5: Run tests**

```bash
cd apps/api
pytest tests/test_executions.py -v
```

Expected: pass.

- [ ] **Step 6: Commit**

```bash
git add apps/api
git commit -m "feat: generate remediation artifacts"
```

### Task 18: Managed-Service Admin Console

**Files:**

- Create: `apps/web/app/(admin)/admin/page.tsx`
- Create: `apps/web/app/(admin)/admin/tasks/page.tsx`
- Create: `apps/api/app/api/routes_admin.py`
- Create: `apps/api/app/services/tasks.py`
- Test: `apps/api/tests/test_admin_tasks.py`

- [ ] **Step 1: Write admin task tests**

Expected:

- consultant can create a task linked to recommendation.
- task can be assigned, updated, completed.

- [ ] **Step 2: Implement admin routes**

Add:

- `GET /api/v1/admin/workspaces`
- `GET /api/v1/admin/tasks`
- `POST /api/v1/admin/tasks`
- `PATCH /api/v1/admin/tasks/{task_id}`

- [ ] **Step 3: Implement admin UI**

Views:

- clients by status.
- pending reports.
- open recommendations.
- tasks due this week.

- [ ] **Step 4: Run tests**

```bash
cd apps/api
pytest tests/test_admin_tasks.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api apps/web
git commit -m "feat: add managed service admin console"
```

### Task 19: QA, Evals, and Cost Guardrails

**Files:**

- Create: `apps/api/app/services/cost_control.py`
- Create: `apps/api/app/evals/extraction_cases.json`
- Create: `apps/api/app/evals/recommendation_cases.json`
- Create: `apps/api/tests/test_cost_control.py`
- Create: `apps/api/tests/test_evals.py`

- [ ] **Step 1: Add cost control tests**

Expected:

- workspace cannot run monitoring if daily cost cap exceeded.
- free checker cannot exceed quota.

- [ ] **Step 2: Add eval fixtures**

Create 20 extraction cases and 10 recommendation cases from synthetic pt-BR examples.

- [ ] **Step 3: Implement eval runner**

The runner should report:

- mention extraction precision/recall.
- citation extraction precision/recall.
- recommendation required fields completeness.

- [ ] **Step 4: Run tests and evals**

```bash
cd apps/api
pytest tests/test_cost_control.py tests/test_evals.py -v
```

Expected: pass.

- [ ] **Step 5: Commit**

```bash
git add apps/api
git commit -m "feat: add qa evals and cost guardrails"
```

### Task 20: Pilot Demo Script and Launch Checklist

**Files:**

- Create: `docs/operations/pilot-demo-script.md`
- Create: `docs/operations/client-onboarding-form.md`
- Create: `docs/operations/monthly-report-playbook.md`
- Create: `docs/product/mvp-launch-checklist.md`

- [ ] **Step 1: Write pilot demo script**

Include:

- lead setup.
- brand onboarding.
- prompt generation.
- monitoring run.
- evidence review.
- audit.
- recommendations.
- report.
- execution artifact.

- [ ] **Step 2: Write onboarding form**

Include:

- brand details.
- competitors.
- locations.
- business goals.
- conversion goals.
- compliance notes.
- integrations.

- [ ] **Step 3: Write monthly report playbook**

Include:

- data refresh.
- consultant review.
- recommendation approval.
- report generation.
- client call agenda.

- [ ] **Step 4: Write launch checklist**

Include:

- all tests pass.
- no auto-publish.
- cost caps enabled.
- API keys configured.
- legal/ToS notes reviewed.
- first pilot client selected.

- [ ] **Step 5: Commit**

```bash
git add docs
git commit -m "docs: add pilot operations playbook"
```

## Verification Commands

Run before declaring the MVP branch complete:

```bash
docker compose up -d postgres redis temporal
cd apps/api && pytest -q
cd apps/web && npm run lint
cd apps/web && npm run test:e2e
```

Expected:

- API tests pass.
- Frontend lint passes.
- Playwright smoke tests pass.
- No test requires live paid APIs unless explicitly marked integration.

## 30-Day Calendar

### Days 1-3

- Bootstrap repo.
- FastAPI foundation.
- Database schema.
- Brand onboarding API.

### Days 4-7

- Prompt generation.
- Prompt approval.
- Basic dashboard onboarding flow.

### Days 8-12

- Provider adapters.
- Monitoring workflow.
- Raw answer storage.
- Extraction.
- Scoring.

### Days 13-17

- Site crawler.
- Technical audit checks.
- Citation/source intelligence.
- Recommendation engine.

### Days 18-21

- Report renderer.
- Free checker.
- Dashboard monitoring/recommendations screens.

### Days 22-25

- Execution artifacts.
- Managed-service admin console.
- Alerts and task workflow.

### Days 26-28

- Evals.
- Cost controls.
- UX polish.
- Report polish.

### Days 29-30

- Run first end-to-end pilot.
- Fix blocking issues.
- Prepare sales demo and paid audit workflow.

## Acceptance Criteria

The MVP is shippable when:

- A consultant can onboard one real Brazilian brand.
- GoRank can generate and approve 30 pt-BR prompts.
- Monitoring runs complete for at least two supported sources/providers or one provider plus manual evidence capture.
- Raw answers, mentions, competitors, citations, and scores are visible.
- Site audit produces findings.
- Recommendations include evidence, confidence, effort, risk, and re-test plan.
- Report can be generated and shared as HTML/PDF.
- Free checker captures leads and returns a sample report.
- No generated content is published automatically.
- Cost caps and rate limits are active.

## Plan Self-Review

- Spec coverage: covers onboarding, prompts, monitoring, citations, audits, recommendations, remediation artifacts, reports, free checker, managed service, cost controls, and QA.
- Completeness scan: no unresolved markers remain.
- Type consistency: API route names and table concepts match the product blueprint.
- Scope check: plan intentionally excludes enterprise features and unsupported automation.
