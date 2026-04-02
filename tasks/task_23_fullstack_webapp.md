---
id: task_23_fullstack_webapp
name: AI-Managed Job Application Submission Website (Long)
category: coding
grading_type: llm_judge
timeout_seconds: 1800
workspace_files: []
---

## Prompt

Build a **production-style web application** in the workspace. Treat the requirements below as the user request.

### Product
Create a full-stack web app called **"ApplyFlow"**: an **AI-managed job application submission and tracking** portal.

The app is used by a job seeker to:
- store a profile/resume,
- manage target companies and job listings,
- generate tailored cover letters,
- track application statuses,
- and submit applications via a configurable workflow.

### Tech stack (choose ONE)
Pick exactly one stack and implement end-to-end:
1. **Python FastAPI + SQLite + Jinja2** (server-rendered)
2. **Python FastAPI + SQLite + React** (SPA)
3. **Node.js (Express) + SQLite + React** (SPA)

Include a dependency manifest (`pyproject.toml`/`requirements.txt` or `package.json`) and a clear `README.md`.

### Functional requirements

#### 1) Authentication & accounts
- Local signup/login (email + password)
- Password hashing
- Session auth (cookies) or JWT
- Basic authorization: users only see their own data

#### 2) Data model (minimum)
Implement entities and relations:
- **UserProfile**: name, email, location, links (GitHub/LinkedIn), skills, years of experience, preferred roles
- **Resume**: upload/store as text or markdown; keep version history (at least 2 versions)
- **Company**: name, industry, location, notes
- **JobPosting**: company_id, title, description, source_url, salary_range (optional), location/remote, created_at
- **Application**: job_posting_id, status (draft/submitted/interview/offer/rejected), submitted_at, next_followup_date
- **Artifact**: generated cover letter / tailored resume snippet per application
- **EventLog**: audit events for create/update/status-change

#### 3) AI features (must be implemented as a module with a clear interface)
Implement an "AI Assistant" service layer that can:
- Generate a **tailored cover letter** from (Profile + Resume + JobPosting)
- Generate a **bullet-point matching analysis**: top 5 matched skills and top 3 gaps
- Produce a **submission checklist** for the application (e.g., missing links, missing portfolio, missing keywords)

Notes:
- If you cannot call real LLM APIs, implement a deterministic placeholder that still produces structured outputs.
- Store AI outputs as `Artifact` records linked to an `Application`.

#### 4) Workflow: “Application Submission” simulation
No real external submissions are required. Instead:
- Provide a **workflow page** for an application that guides the user through steps:
  1) review posting,
  2) generate artifacts,
  3) confirm checklist,
  4) mark as submitted,
  5) schedule follow-up.
- Each step should update state and write an `EventLog` entry.

#### 5) Search & analytics
- Search job postings by title/description/company
- Filter applications by status and date range
- Dashboard with at least:
  - counts by status,
  - applications per week chart,
  - response rate (interview/offer vs submitted) computed from existing records.

#### 6) Import/Export
- Export all user data to a single JSON file (`export.json`)
- Import from JSON with validation and meaningful error messages

#### 7) UX requirements
- Modern responsive UI
- Basic navigation (sidebar/topbar)
- Form validation and error messaging
- Provide seed/sample data to demonstrate the workflow end-to-end

#### 8) Quality
- Clear code organization (routes/controllers, models/schema, services)
- DB initialization or migrations
- Minimal automated tests covering at least:
  - auth login flow OR
  - creating an application + generating an artifact.

### Deliverables
At minimum, create:
- The runnable app source code
- `README.md` with:
  - install instructions
  - DB init/migrate instructions
  - run instructions
  - test instructions
- Seed script or documented steps to create sample data

### Expected runtime
This is a long task. A complete solution should take substantial time to implement (~30 minutes).

## Grading (LLM Judge only, 100%)

Score from **0.0 to 1.0** based on:
- App runs from the repo with correct setup docs
- Auth + authorization correctness
- Data model completeness
- AI service layer + stored artifacts
- Workflow simulation correctness
- Search/filter/dashboard analytics exist and look reasonable
- Import/export with validation
- UI quality and usability
- Tests exist and are meaningful
