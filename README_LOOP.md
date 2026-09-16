# LOOP — AI Customer Feedback Intelligence Platform

> **Turn scattered customer feedback into clear, evidence-backed product decisions.**

LOOP is a full-stack, multi-tenant customer-feedback intelligence platform that brings customer feedback into one place, classifies it with Google Gemini, identifies themes and trends, supports semantic search and retrieval-grounded Q&A, and generates Voice-of-Customer reports.

The application connects the complete feedback lifecycle:

```text
Feedback Ingestion
        ↓
Feedback Inbox
        ↓
AI Classification
        ↓
Themes & Trends
        ↓
Semantic Search / Ask LOOP
        ↓
Voice-of-Customer Reports
        ↓
Evidence-backed Decisions
```

---

## 🚀 Project Highlights

- 🔐 Multi-tenant workspace architecture
- 👥 Role-based access control
- 📥 Manual feedback entry
- 📄 CSV bulk feedback import
- 🔄 Demo/simulated feedback channel ingestion
- 🧠 Google Gemini-powered classification
- 😊 Sentiment analysis and sentiment scoring
- 🏷️ AI-assisted theme assignment
- 📈 Theme and trend analytics
- 🔎 Semantic search using PostgreSQL + pgvector
- 💬 Retrieval-grounded **Ask LOOP**
- 📊 Analytics dashboard
- 📑 Voice-of-Customer report generation
- 🔗 Secure read-only report sharing
- 🛡️ Server-side authorization and workspace isolation
- 💾 Persisted AI classifications and embeddings

---

# 📌 Quick Links

| Resource | Location |
|---|---|
| 🌐 Application | `http://localhost:3000` |
| 💻 GitHub Repository | Your Project LOOP repository |
| 📚 Documentation | `loop/docs/` |
| 🖼️ Screenshots | `loop/docs/screenshots/` |
| ⚙️ Environment Template | `loop/.env.example` |

---

# 🖥️ Product Preview

## Login

![Login](loop/docs/screenshots/01-login.png)

## Dashboard

![Dashboard](loop/docs/screenshots/02-dashboard.png)

## Feedback Inbox

![Feedback Inbox](loop/docs/screenshots/03-inbox.png)

## Themes

![Themes](loop/docs/screenshots/04-themes.png)

## Trends

![Trends](loop/docs/screenshots/05-trends.png)

## Ask LOOP

![Ask LOOP](loop/docs/screenshots/06-ask-loop.png)

## Voice-of-Customer Report

![Voice-of-Customer Report](loop/docs/screenshots/07-voc-report.png)

## Admin / Members

![Admin Members](loop/docs/screenshots/08-admin-members.png)

---

# 🎯 What is LOOP?

LOOP is designed for teams that receive customer feedback from multiple sources such as:

- Support tickets
- Live chat
- Application reviews
- NPS surveys
- CSAT surveys
- Sales call notes
- Community posts
- Social mentions
- CSV imports
- Simulated/demo channels

Instead of manually reading and organizing large amounts of customer feedback, LOOP centralizes the information and applies AI-assisted analysis to turn raw comments into useful product intelligence.

---

# ❗ The Problem

Customer feedback is often:

- scattered across different channels
- difficult to search
- manually classified
- inconsistent in tagging
- difficult to prioritize
- disconnected from product decisions
- too large to analyze manually

LOOP addresses this by creating a single workflow for collecting, classifying, analyzing, retrieving, and reporting customer feedback.

---

# 💡 The Solution

```text
Customer Feedback
       ↓
Centralized Inbox
       ↓
AI Classification
       ↓
Sentiment + Themes
       ↓
Trend Analysis
       ↓
Semantic Retrieval
       ↓
Ask LOOP
       ↓
Voice-of-Customer Reports
```

The objective is to make customer feedback easier to understand and connect insights back to the original evidence.

---

# ⭐ Key Features

## 1. 🔐 Multi-Tenant Workspaces

LOOP supports workspace-based data isolation.

Workspace-related data includes:

- Users
- Feedback
- Themes
- Embeddings
- Reports
- Invitations

The authenticated user's workspace is resolved server-side so client-provided workspace identifiers are not treated as the authoritative tenant boundary.

---

## 2. 👥 Role-Based Access Control

LOOP supports three application roles:

| Role | Access |
|---|---|
| **ADMIN** | Workspace administration and full product access |
| **ANALYST** | Feedback and intelligence workflows |
| **VIEWER** | Read-only analytics and insight access |

Authorization is implemented on the server.

---

## 3. 📥 Feedback Ingestion

Feedback can be added through:

### Single Entry

Users can enter one customer comment at a time.

The form captures:

- Feedback content
- Channel
- Customer label
- Source reference

Customer label and source reference are optional.

### CSV Upload

Bulk feedback can be imported from CSV files.

The import workflow validates rows and provides imported/failed summaries.

### Demo Channel

The project also includes a simulated/demo ingestion workflow for evaluating the application without requiring external feedback-provider integrations.

---

# 📬 Feedback Inbox

The Feedback Inbox provides a centralized location for searching and managing customer feedback.

Supported capabilities include:

- Server-side pagination
- Search
- Channel filtering
- Sentiment filtering
- Theme filtering
- Workflow-status filtering
- Date filtering
- Combined filters
- Inline workflow actions
- Manual classification retry

### Workflow

```text
NEW
 ↓
REVIEWED
 ↓
ACTIONED
```

Feedback classification status is also tracked separately so users can identify pending, completed, or failed AI processing.

---

# 📊 Analytics Dashboard

The dashboard provides an overview of customer feedback using persisted database data.

It includes:

- Total feedback
- Negative feedback percentage
- New feedback this week
- Classification coverage
- Feedback volume over time
- Sentiment breakdown
- Top themes
- Average sentiment score
- Theme coverage
- Classification state
- Workflow filtering

Dashboard filters can be applied by:

- Date range
- Channel
- Workflow status

---

# 🧠 Google Gemini AI Classification

LOOP uses Google Gemini for AI-powered feedback classification.

The classification pipeline is designed around structured output validation:

```text
Customer Feedback
       ↓
Google Gemini
       ↓
Structured Response
       ↓
Validation
       ↓
Persisted Classification
```

A classification can contain:

- Sentiment
- Sentiment score
- Theme information
- Theme confidence
- Feature-area information
- Grounded rationale

The sentiment score is represented on a scale from:

```text
-1  ← Negative
 0  ← Neutral
+1  ← Positive
```

AI results are persisted in PostgreSQL so they do not need to be regenerated every time the UI loads.

---

# 🏷️ Theme Intelligence

LOOP groups customer feedback into higher-level themes.

Theme functionality includes:

- Theme creation
- Theme search
- Theme sorting
- AI-assisted theme assignment
- Existing-theme reuse
- Theme counts
- Assignment confidence
- Feedback evidence drill-down

This helps teams move from individual customer comments to recurring product areas.

---

# 📈 Trends

The Trends section provides time-based theme intelligence.

It can be used to understand:

- Current theme volume
- Previous-period theme volume
- Changes in theme activity
- Emerging themes
- Increasing feedback areas

The application contains configured logic for identifying themes that meet minimum count, absolute-growth, and percentage-growth conditions.

---

# 💬 Ask LOOP

**Ask LOOP** provides retrieval-grounded natural-language Q&A over customer feedback.

Example:

> What are customers saying about onboarding?

Instead of sending the question directly to an AI model, LOOP follows a retrieval workflow:

```text
User Question
      ↓
Generate Query Embedding
      ↓
PostgreSQL + pgvector
      ↓
Retrieve Relevant Feedback
      ↓
Send Retrieved Evidence to Gemini
      ↓
Generate Structured Answer
      ↓
Validate Evidence References
      ↓
Display Answer + Supporting Feedback
```

This approach helps keep answers connected to actual feedback stored in the workspace.

If the available evidence does not support an answer, the application is designed to avoid presenting unsupported information as customer evidence.

---

# 🔎 Semantic Search

LOOP uses vector embeddings to support semantic retrieval.

The architecture uses:

- Google Gemini embeddings
- PostgreSQL
- pgvector
- Workspace-scoped feedback retrieval

Embeddings are stored in the database and can be reused for subsequent retrieval operations.

---

# 📄 Voice-of-Customer Reports

LOOP can generate Voice-of-Customer reports from customer feedback.

Reports can contain:

- Feedback totals
- Classification coverage
- Sentiment distribution
- Sentiment changes
- Top themes
- Representative feedback
- Executive narrative
- Recommended actions
- Evidence references

The numerical statistics are calculated from application/database data before AI-generated narrative content is created.

Reports can be:

- Generated
- Saved
- Viewed later
- Searched
- Shared through read-only links

---

# 🔗 Report Sharing

Reports can be exposed through secure read-only sharing links.

The sharing capability is intended for situations where a report needs to be reviewed without granting access to the complete LOOP workspace.

---

# 🛡️ Security

LOOP includes several server-side security patterns.

## Workspace Isolation

Workspace ownership is resolved from the authenticated session.

## Server-Side Authorization

Protected actions verify the user's role before allowing access.

## AI Credentials

The Gemini API key is intended to remain server-side.

Do **not** expose it through:

```text
NEXT_PUBLIC_*
```

## Environment Files

Never commit the real `.env` file to GitHub.

Only commit the example configuration:

```text
.env.example
```

---

# 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| **Next.js** | Full-stack web application |
| **React** | User interface |
| **TypeScript** | Application development |
| **Tailwind CSS** | UI styling |
| **PostgreSQL** | Relational database |
| **Prisma** | ORM and migrations |
| **pgvector** | Vector/semantic search |
| **Google Gemini** | AI classification and embeddings |
| **NextAuth.js** | Authentication |
| **Zod** | Input/output validation |
| **Recharts** | Analytics visualizations |
| **bcryptjs** | Password hashing |
| **CSV Parse** | CSV import processing |
| **PDFKit** | Report/PDF generation |

---

# 📋 Requirements

Before running LOOP locally, install:

- Node.js `18.18+`
- npm
- PostgreSQL
- pgvector PostgreSQL extension
- Git
- A Google Gemini API key

Recommended:

- VS Code
- pgAdmin 4

---

# 🚀 Local Development

## 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Then enter the project directory.

```bash
cd Project-loop-main
cd loop
```

> The application code is located inside the `loop` directory.

---

# 2. Install dependencies

Run:

```bash
npm install
```

This installs the project dependencies and generates the Prisma Client through the configured post-install workflow.

---

# 3. Configure environment variables

Create:

```text
.env
```

using `.env.example` as the template.

Example:

```env
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/project-loop_db"
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="replace-with-a-random-secret"
GEMINI_API_KEY="replace-with-your-gemini-api-key"

SEED_ADMIN_PASSWORD="replace-with-admin-password"
SEED_ANALYST_PASSWORD="replace-with-analyst-password"
SEED_VIEWER_PASSWORD="replace-with-viewer-password"
```

### Important

Do not put a real Gemini API key into:

- GitHub README
- GitHub source files
- screenshots
- public environment variables
- client-side JavaScript

---

# 4. Create the PostgreSQL database

Create a PostgreSQL database named:

```text
project-loop_db
```

The database user and password must match the values used in `DATABASE_URL`.

---

# 5. Enable pgvector

LOOP requires the PostgreSQL `vector` extension for semantic embeddings.

After pgvector is installed on the PostgreSQL server, connect to the LOOP database and run:

```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

You can verify the extension with:

```sql
SELECT * FROM pg_extension WHERE extname = 'vector';
```

If PostgreSQL reports:

```text
extension "vector" is not available
```

pgvector must first be installed on the PostgreSQL server.

---

# 6. Validate the Prisma schema

Run:

```bash
npm run db:validate
```

Expected result:

```text
The schema at prisma\schema.prisma is valid
```

---

# 7. Apply database migrations

Run:

```bash
npm run db:migrate
```

If this is a fresh development database and Prisma reports schema drift caused by an existing development database, use the reset workflow only when you are sure the database contains no data that must be preserved:

```bash
npm run db:reset
```

---

# 8. Seed the database

The project contains a seed script for creating demo workspace data.

Run:

```bash
npm run db:seed
```

The seed passwords must satisfy the application's password-length requirements.

---

# 9. Start the development server

Run:

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

The application login page is:

```text
http://localhost:3000/login
```

---

# 🔑 Demo Accounts

The seed process creates demo roles.

Use the credentials printed by the seed command.

Example format:

```text
ADMIN
admin@loop.demo
<seeded admin password>

ANALYST
analyst@loop.demo
<seeded analyst password>

VIEWER
viewer@loop.demo
<seeded viewer password>
```

> Do not publish real passwords in a public repository. Configure seeded passwords through `.env`.

---

# 🗃️ Database Commands

## Generate Prisma Client

```bash
npm run prisma:generate
```

## Validate schema

```bash
npm run db:validate
```

## Format Prisma schema

```bash
npm run db:format
```

## Create/apply development migration

```bash
npm run db:migrate
```

## Deploy existing migrations

```bash
npm run db:migrate:deploy
```

## Reset development database

```bash
npm run db:reset
```

> Reset deletes development database data.

## Open Prisma Studio

```bash
npm run db:studio
```

---

# 🤖 AI Commands

## Verify AI connectivity

```bash
npm run ai:verify
```

## Backfill classifications

```bash
npm run ai:backfill
```

## Backfill embeddings

```bash
npm run ai:backfill-embeddings
```

## Prepare classified demo data

```bash
npm run db:seed:classified
```

## Prepare complete demo data

```bash
npm run db:seed:ready
```

## Seed and verify final demo dataset

```bash
npm run db:seed:final
```

---

# 🧪 Verification & QA

The project contains several verification commands.

### TypeScript

```bash
npm run typecheck
```

### Formatting

```bash
npm run format:check
```

### Build

```bash
npm run build
```

### AI verification

```bash
npm run ai:verify
```

### Database seed verification

```bash
npm run db:verify:seed
```

### Repository QA

```bash
npm run qa:repo
```

### Final QA

```bash
npm run final:qa
```

### Submission QA

```bash
npm run qa:submission
```

### Smoke test

```bash
npm run smoke -- --base-url=http://localhost:3000
```

---

# 📂 Project Structure

```text
Project-loop-main/
└── loop/
    ├── app/
    │   ├── (auth)/
    │   │   ├── invite/
    │   │   ├── login/
    │   │   └── signup/
    │   │
    │   ├── (app)/
    │   │   ├── ask/
    │   │   ├── dashboard/
    │   │   ├── inbox/
    │   │   ├── profile/
    │   │   ├── reports/
    │   │   ├── settings/
    │   │   ├── themes/
    │   │   └── trends/
    │   │
    │   ├── about/
    │   ├── api/
    │   └── shared/
    │
    ├── components/
    ├── docs/
    │   └── screenshots/
    │
    ├── lib/
    ├── prisma/
    │   ├── migrations/
    │   ├── schema.prisma
    │   ├── seed-data.ts
    │   └── seed.ts
    │
    ├── public/
    ├── scripts/
    ├── services/
    ├── types/
    │
    ├── .env.example
    ├── next.config.mjs
    ├── package.json
    ├── tailwind.config.ts
    └── tsconfig.json
```

---

# 🗄️ Prisma Data Model

The Prisma schema contains the following major models:

```text
Workspace
User
WorkspaceInvitation
Feedback
Theme
FeedbackTheme
Embedding
Report
```

Important enum types include:

```text
UserRole
FeedbackChannel
FeedbackSentiment
FeedbackStatus
ClassificationStatus
```

The database therefore supports authentication, workspaces, feedback, AI classification, themes, embeddings, invitations, and reports.

---

# 🔌 API Areas

The application includes Next.js Route Handlers for major workflows such as:

- Authentication
- User registration
- Dashboard analytics
- Feedback creation
- Feedback search/filtering
- CSV feedback import
- Feedback classification
- Theme management
- Trends
- Reports
- Report sharing
- Ask LOOP
- Workspace/member management

API routes are protected according to the authenticated workspace and user role.

---

# 🧠 AI Architecture

The AI-related workflow can be summarized as:

```text
                    ┌──────────────────┐
                    │ Customer Feedback│
                    └────────┬─────────┘
                             │
                 ┌───────────▼───────────┐
                 │   Feedback Service    │
                 └───────────┬───────────┘
                             │
                  ┌──────────▼──────────┐
                  │   Google Gemini     │
                  │ Classification /    │
                  │ Embeddings           │
                  └───────┬───────┬──────┘
                          │       │
                  Classification Embedding
                          │       │
                    ┌─────▼──┐ ┌─▼────────┐
                    │Postgres│ │ pgvector │
                    └─────┬──┘ └────┬─────┘
                          │          │
                  ┌───────▼──────────▼──────┐
                  │ Dashboard / Themes /    │
                  │ Trends / Ask LOOP /     │
                  │ Reports                 │
                  └─────────────────────────┘
```

---

# 💬 Ask LOOP Architecture

```text
Question
   ↓
Query Validation
   ↓
Gemini Embedding
   ↓
pgvector Similarity Search
   ↓
Workspace-scoped Feedback
   ↓
Retrieved Evidence
   ↓
Gemini Response Generation
   ↓
Evidence Validation
   ↓
Answer + Supporting Feedback
```

This makes the Q&A workflow retrieval-grounded instead of relying only on the language model's general knowledge.

---

# 📊 Reporting Architecture

The report workflow follows:

```text
Selected Date Range
        ↓
Database Query
        ↓
Deterministic Statistics
        ↓
Sentiment / Theme Analysis
        ↓
Representative Feedback
        ↓
Gemini Narrative Generation
        ↓
Saved Voice-of-Customer Report
        ↓
Optional Read-only Sharing
```

This separates numerical calculations from AI-generated narrative content.

---

# 🖼️ Screenshot Gallery

| Screen | File |
|---|---|
| Login | `loop/docs/screenshots/01-login.png` |
| Dashboard | `loop/docs/screenshots/02-dashboard.png` |
| Inbox | `loop/docs/screenshots/03-inbox.png` |
| Themes | `loop/docs/screenshots/04-themes.png` |
| Trends | `loop/docs/screenshots/05-trends.png` |
| Ask LOOP | `loop/docs/screenshots/06-ask-loop.png` |
| Voice-of-Customer Report | `loop/docs/screenshots/07-voc-report.png` |
| Admin Members | `loop/docs/screenshots/08-admin-members.png` |
| Report Preview 1 | `loop/docs/screenshots/report-1.png` |
| Report Preview 2 | `loop/docs/screenshots/report-2.png` |

---

# ⚙️ Environment Variables

| Variable | Required | Purpose |
|---|---:|---|
| `DATABASE_URL` | Yes | PostgreSQL connection |
| `NEXTAUTH_URL` | Yes | Application origin |
| `NEXTAUTH_SECRET` | Yes | Authentication/session protection |
| `GEMINI_API_KEY` | Yes | Google Gemini access |
| `SEED_ADMIN_PASSWORD` | No | Seeded Admin password |
| `SEED_ANALYST_PASSWORD` | No | Seeded Analyst password |
| `SEED_VIEWER_PASSWORD` | No | Seeded Viewer password |

Example:

```env
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/project-loop_db"
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="replace-with-a-random-secret"
GEMINI_API_KEY="replace-with-your-gemini-api-key"
SEED_ADMIN_PASSWORD="replace-with-admin-password"
SEED_ANALYST_PASSWORD="replace-with-analyst-password"
SEED_VIEWER_PASSWORD="replace-with-viewer-password"
```

---

# 🐛 Common Issues

## 1. `extension "vector" is not available`

LOOP requires pgvector.

Install pgvector for the PostgreSQL version being used and then run:

```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

---

## 2. Prisma says `Workspace` or `User` table does not exist

Apply the migrations:

```bash
npm run db:migrate
```

For a disposable development database:

```bash
npm run db:reset
```

---

## 3. Gemini API key is invalid

Check `.env`:

```env
GEMINI_API_KEY="YOUR_REAL_GEMINI_API_KEY"
```

Do not use:

```env
GEMINI_API_KEY="YOUR_ACTUAL_GEMINI_API_KEY"
```

or:

```env
GEMINI_API_KEY="your-real-key-here"
```

After changing `.env`, restart the Next.js development server:

```bash
npm run dev
```

---

## 4. Application returns HTTP 500 after changing `.env`

Stop the development server and start it again.

```text
Ctrl + C
```

Then:

```bash
npm run dev
```

Environment variables are loaded by the server process.

---

## 5. `npm run dev` says `package.json` cannot be found

Make sure the terminal is inside:

```text
Project-loop-main\loop
```

Check with:

```bash
dir package.json
```

You should see the project's `package.json`.

---

# 📦 Available npm Scripts

```text
npm run dev
npm run start
npm run build
npm run lint
npm run typecheck
npm run format
npm run format:check

npm run prisma:generate

npm run db:validate
npm run db:format
npm run db:migrate
npm run db:migrate:deploy
npm run db:reset
npm run db:seed
npm run db:studio

npm run seed

npm run ai:verify
npm run ai:backfill
npm run ai:backfill-embeddings

npm run db:seed:classified
npm run db:seed:ready
npm run db:verify:seed
npm run db:seed:final

npm run smoke
npm run qa:repo
npm run qa:submission
npm run final:qa
```

---

# 🚀 Production / Deployment

LOOP is structured as a Next.js application and can be deployed to a suitable Node.js hosting platform with:

- Next.js support
- PostgreSQL
- pgvector
- Secure environment variables

Before deployment:

### 1. Configure production environment

```text
DATABASE_URL
NEXTAUTH_URL
NEXTAUTH_SECRET
GEMINI_API_KEY
```

Seed-related variables should only be configured when required for the deployment workflow.

### 2. Apply migrations

```bash
npm run db:migrate:deploy
```

### 3. Build the application

```bash
npm run build
```

### 4. Start the production server

```bash
npm run start
```

---

# 🔒 GitHub Security Checklist

Before pushing this project to GitHub:

- [ ] `.env` is not committed
- [ ] Real Gemini API keys are removed from files
- [ ] Real passwords are not included
- [ ] Database passwords are not included
- [ ] API tokens are not included
- [ ] `.gitignore` contains `.env`
- [ ] Only `.env.example` is committed
- [ ] Screenshots do not expose secrets
- [ ] GitHub secret scanning shows no exposed credentials

---

# 📝 Development Notes

The application is organized around several service layers:

```text
UI
 ↓
API Route Handlers
 ↓
Services
 ↓
Prisma / PostgreSQL
 ↓
AI / Vector Services
```

This separation keeps application workflows separate from the presentation layer and database access.

---

# 🔮 Possible Future Enhancements

Potential future improvements include:

- Additional real-world feedback integrations
- Saved inbox views and segments
- Automated sentiment alerts
- Suggested product actions
- Expanded automated API tests
- Additional AI providers
- Advanced analytics and reporting
- More granular workspace permissions
- Production monitoring and observability

---

# 📄 Project Scope

LOOP focuses on the customer-feedback intelligence workflow.

The current implementation is centered on:

```text
Ingestion
Classification
Theme Intelligence
Trend Analysis
Semantic Retrieval
Ask LOOP
Reporting
Workspace Management
```

External integrations that are not implemented in the current codebase should not be treated as existing functionality.

---

# 📚 Documentation

Additional project documentation is available under:

```text
loop/docs/
```

Screenshot documentation is available under:

```text
loop/docs/screenshots/
```

---

# 👨‍💻 Project

**Project:** LOOP — AI Customer Feedback Intelligence Platform

**Application type:** Full-stack AI-powered customer feedback intelligence platform

**Primary stack:** Next.js + TypeScript + PostgreSQL + Prisma + pgvector + Google Gemini

**Development environment:** Local Node.js + PostgreSQL

---

# 📜 License

No open-source license is currently declared for this project.

Unless a separate license is added to the repository, the project should be treated as having no explicit open-source redistribution license.

---

## ⭐ LOOP

> **Close the loop between customer feedback, product insight, and action.**
