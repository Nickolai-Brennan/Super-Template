## Published in this repository

### Core docs
- `docs/project-charter.md`
- `docs/roadmap.md`
- `docs/adrs/README.md`
- `docs/runbooks/README.md`
- `guidelines/copilot-agent-governance.md`

### Templates
- `templates/project-charter-template.md`
- `templates/roadmap-template.md`
- `templates/adr-template.md`
- `templates/runbook-template.md`

---

Below is the working Project Planning + Tech Docs Catalog for Damn You Docs, cut for serious MVP execution. It keeps the full control-plane logic from the Master Control File and avoids the 180-doc overbuild trap.  

Damn You Docs — Project Planning Catalog

0. Control Docs

Doc	Purpose	Priority

MASTER_CONTROL_FILE.md	Source of truth for all docs, tasks, and execution status	P0
README.md	Repo/project orientation	P0
PROJECT_OVERVIEW.md	What the product is, who it serves, and why it exists	P0
VISION_AND_GOALS.md	Product vision, success metrics, strategic direction	P1
DECISION_LOG.md	Tracks major architecture/product decisions	P1


1. Product Planning

Doc	Purpose	Priority

PRODUCT_BRIEF.md	One-page product summary	P0
PROBLEM_STATEMENT.md	Defines the documentation pain being solved	P0
TARGET_AUDIENCE.md	ICP, user types, buyer/user split	P0
VALUE_PROPOSITION.md	Core positioning and differentiation	P0
MVP_DEFINITION.md	Locks must-have vs later features	P0
FEATURE_LIST.md	Full feature inventory by phase	P0
ROADMAP.md	Phase-based delivery plan	P0
PRICING_AND_MONETIZATION.md	Free/Pro/Team/Enterprise model	P1


2. MVP Execution Planning

Doc	Purpose	Priority

BUILD_PLAN.md	Week-by-week implementation plan	P0
SPRINT_BACKLOG.md	Active tasks for current build cycle	P0
RELEASE_PLAN.md	What ships in v0.1, v0.2, v1.0	P1
SCOPE_CHANGE_LOG.md	Prevents silent feature creep	P1
RISK_REGISTER.md	Tracks risks: scope creep, UX gaps, GitHub sync complexity	P1


Tech Docs Catalog

3. System Architecture

Doc	Purpose	Priority

SYSTEM_ARCHITECTURE_OVERVIEW.md	High-level app architecture	P0
FRONTEND_ARCHITECTURE.md	React app structure, routes, state, components	P0
BACKEND_ARCHITECTURE.md	FastAPI/GraphQL service structure	P0
DATABASE_ARCHITECTURE.md	PostgreSQL schema strategy	P0
INTEGRATIONS_AND_APIS.md	GitHub sync, custom domains, webhooks	P1
AI_ARCHITECTURE.md	AI writer/search/meta generation architecture	P2


4. Frontend Docs

Doc	Purpose	Priority

FRONTEND_TECH_STACK.md	React, PrimeReact, PrimeBlocks, TanStack	P0
PAGE_DIRECTORY.md	Landing, dashboard, editor, analytics, settings	P0
COMPONENT_LIBRARY.md	Reusable UI components	P0
DESIGN_SYSTEM.md	Colors, typography, spacing, layout rules	P0
STATE_MANAGEMENT.md	App state, editor state, auth state	P1
FRONTEND_BUILD_PROCESS.md	Local build, linting, deployment commands	P1


5. Backend/API Docs

Doc	Purpose	Priority

BACKEND_TECH_STACK.md	FastAPI, GraphQL, PostgreSQL, Docker	P0
API_OVERVIEW.md	API structure and conventions	P0
API_ENDPOINTS.md	REST/GraphQL endpoint catalog	P0
GRAPHQL_SCHEMA.md	Types, queries, mutations	P1
API_AUTHENTICATION.md	Login/session/API key model	P0
ERROR_HANDLING.md	API and backend error format	P1
RATE_LIMITING_AND_SECURITY.md	Abuse prevention and access limits	P1


6. Database/Data Docs

Doc	Purpose	Priority

DATABASE_OVERVIEW.md	Data model summary	P0
ERD.md	Entity relationship diagram	P0
TABLE_DEFINITIONS.md	Tables, fields, indexes	P0
MIGRATIONS_AND_VERSIONING.md	Schema migration process	P1
DATA_VALIDATION_RULES.md	Required fields, constraints, normalization	P1
ANALYTICS_SCHEMA.md	Events, page views, search analytics	P1


7. Core Feature Specs

Doc	Purpose	Priority

FEATURE_PROJECT_CREATION.md	Project/workspace creation	P0
FEATURE_PAGE_CREATION.md	Docs page CRUD	P0
FEATURE_TEMPLATES.md	Template library and insertion	P0
FEATURE_EDITOR.md	WYSIWYG/Markdown editor behavior	P0
FEATURE_PUBLISHING.md	Draft/publish/version states	P0
FEATURE_ANALYTICS.md	Basic page views/search analytics	P0
FEATURE_CUSTOM_DOMAIN.md	Domain/subdomain setup	P1
FEATURE_GITHUB_SYNC.md	Push/pull sync model	P1
FEATURE_AI_WRITER.md	AI writing assistant	P2
FEATURE_AI_SEARCH.md	AI-powered search	P2


8. DevOps/Environment

Doc	Purpose	Priority

LOCAL_DEV_SETUP.md	Local install/run instructions	P0
ENVIRONMENT_VARIABLES.md	Required env vars	P0
DOCKER_SETUP.md	Docker services and compose setup	P1
CI_CD_PIPELINE.md	Tests/build/deploy pipeline	P1
DEPLOYMENT_GUIDE.md	Vercel/Railway/Render deployment	P1
MONITORING_AND_LOGGING.md	Logs, uptime, errors	P2
BACKUP_AND_RECOVERY.md	Database backup/restore	P2


9. Security Docs

Doc	Purpose	Priority

SECURITY_OVERVIEW.md	Security model summary	P1
AUTHORIZATION_MODEL.md	Roles, permissions, project access	P1
DATA_PRIVACY.md	User data handling	P1
AUDIT_LOGGING.md	Track sensitive actions	P2
THREAT_MODEL.md	Risks and mitigations	P2


10. QA/Launch Docs

Doc	Purpose	Priority

TESTING_STRATEGY.md	Overall testing approach	P1
UNIT_TESTS.md	Unit test coverage targets	P1
INTEGRATION_TESTS.md	API/database tests	P1
E2E_TESTS.md	Critical user flows	P1
BUG_TRACKING_PROCESS.md	Bug intake and triage	P1
LAUNCH_CHECKLIST.md	Final MVP launch gate	P0


Recommended MVP Doc Set

Build these first:

1. MASTER_CONTROL_FILE.md


2. README.md


3. PROJECT_OVERVIEW.md


4. PRODUCT_BRIEF.md


5. MVP_DEFINITION.md


6. FEATURE_LIST.md


7. ROADMAP.md


8. SYSTEM_ARCHITECTURE_OVERVIEW.md


9. FRONTEND_ARCHITECTURE.md


10. BACKEND_ARCHITECTURE.md


11. DATABASE_OVERVIEW.md


12. ERD.md


13. API_OVERVIEW.md


14. API_ENDPOINTS.md


15. FEATURE_EDITOR.md


16. FEATURE_TEMPLATES.md


17. FEATURE_PUBLISHING.md


18. FEATURE_GITHUB_SYNC.md


19. LOCAL_DEV_SETUP.md


20. LAUNCH_CHECKLIST.md



This gives you a complete MVP documentation spine without drowning the project in unused enterprise docs.
