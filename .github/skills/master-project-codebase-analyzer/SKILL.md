---
name: master-project-codebase-analyzer
description: "Use when analyzing an unfamiliar repository to produce a codebase master map: architecture, file responsibilities, feature coverage, technology stack, implementation status, gaps, risks, and modification guidance grounded in actual repository evidence."
---

# Master Project Codebase Analyzer

## Purpose

Analyze a real software project or repository and produce a comprehensive CODEBASE MASTER MAP.

This skill acts like a senior software architect and codebase archaeologist: it inspects the implementation, traces the actual structure and behavior, and explains how the project works without relying on marketing docs, assumptions, or filenames alone.

It is designed to answer:
- What is this project?
- Why does it exist?
- What problem does it solve?
- Who uses it?
- What technologies are actually used?
- How is the system structured?
- What does every important file do?
- How do modules communicate?
- How does data flow?
- Where is each feature implemented?
- What is implemented vs incomplete vs missing?
- What should a developer inspect before making changes?

## Core Operating Principle

"Understand the repository from evidence, map the architecture, connect every important file to its responsibility, and produce a reliable master map that another developer can use to understand and modify the project."

## Mandatory Constraints

Before producing conclusions, the analysis must:

1. Inspect the actual repository contents and source code.
2. Cross-check documentation against implementation.
3. Trace imports, exports, routes, services, APIs, hooks, components, utilities, and configuration.
4. Distinguish between documented, implemented, partial, missing, unused, and planned behavior.
5. Never invent features or architecture not supported by repository evidence.
6. Never expose secrets, credentials, tokens, passwords, private environment values, or keys.
7. Ignore generated/build/cache/dependency folders when they are not helpful to understanding the architecture.
8. When uncertain, explicitly say: "Unclear / Needs Verification".
9. Always provide exact file paths when describing implementation.
10. Do not modify the repository while analyzing it unless the user explicitly asks for a code change.

## Required Analysis Method

Follow this workflow in order.

### Step 1: Establish the repository reality

- Inspect the root structure.
- Identify the project type: frontend, backend, full-stack, library, CLI, service, monorepo, desktop, etc.
- Read only meaningful files first:
  - package manifests
  - build configs
  - framework config
  - runtime config
  - main app entrypoints
  - routes and controllers
  - database definitions
  - auth logic
  - major services
- Skip generated folders and dependency outputs unless they directly reveal runtime behavior.

### Step 2: Verify the actual technology stack

Use repository evidence, not assumptions.

Check for:
- Languages and runtimes
- Frontend framework or library
- Backend runtime and framework
- Databases and ORM or query layer
- Authentication strategy
- API layer
- State management approach
- Styling system
- Test framework
- Build and deployment tools
- External services and integrations

For each technology, identify:
- Where it is configured or imported
- Where it is used in code
- Whether it is active or merely declared

### Step 3: Map the actual structure

Build a meaningful repository map covering:
- source
- frontend
- backend
- database
- components
- pages/routes
- services
- utilities
- configuration
- tests
- scripts
- docs
- deployment
- assets

Do not waste space on generated dependency files.

### Step 4: Trace the architecture from code, not docs

Follow the actual flow of execution:
- entry point → routes/pages → components → hooks/state → services → API/backend → database/external service → response → UI

Trace:
- imports/exports
- route definitions
- API endpoints
- service calls
- component composition
- data schema usage
- config wiring
- auth guards and middleware

### Step 5: Identify implementation status

Classify everything as:
- 🟢 IMPLEMENTED
- 🟡 PARTIALLY IMPLEMENTED
- 🔴 MISSING
- ⚪ PLACEHOLDER / UNUSED
- 🔵 PLANNED / DOCUMENTED ONLY

Use actual evidence from the repository and avoid optimistic interpretation.

### Step 6: Compare docs to reality

Check for discrepancies between:
- README and implementation
- package dependencies and actual imports
- documented features and implemented features
- configuration and runtime behavior
- deployment docs and real deployment files

Report the contradiction clearly when found.

### Step 7: Discover gaps, risks, and debt

Search for:
- TODO / FIXME / HACK
- dead code
- broken imports
- placeholder values
- duplicated logic
- inconsistent naming
- missing validation or error handling
- unused dependencies
- suspicious hardcoded config
- type mismatches
- unimplemented services or routes

### Step 8: Build the master summary

Produce the required sections in the output format below, ensuring each section is grounded in real repository evidence.

## Required Output Structure

The final output must include these sections in order.

# 1. EXECUTIVE SUMMARY

Explain:
- Project name
- Project purpose
- Problem solved
- Target users
- Core functionality
- Current maturity
- One-sentence description
- Five-sentence explanation
- Detailed explanation

# 2. ACTUAL TECHNOLOGY STACK

Create a table like:

| Layer | Technology | Version | Evidence/File | Purpose |
|------|------------|---------|---------------|---------|

Only include technologies evidenced by the repository.

Cover:
- Languages
- Frontend
- Backend
- Frameworks
- Database
- ORM
- Authentication
- APIs
- Styling
- State management
- Build tools
- Testing
- Deployment
- External services
- Important libraries

# 3. COMPLETE PROJECT STRUCTURE

Create a meaningful directory tree.

Explain every important directory.

Separate:
- source
- frontend
- backend
- database
- components
- pages/routes
- services
- utilities
- configuration
- tests
- scripts
- documentation
- deployment
- assets

# 4. FILE-BY-FILE RESPONSIBILITY MAP

For every important file:

### `path/to/file`

- Purpose
- Responsibility
- Main functions/classes/components
- Inputs
- Outputs
- Imports
- Consumers
- Dependencies
- Architectural role
- Status
- Important notes

Answer: "WHAT DOES THIS FILE ACTUALLY DO?"

# 5. ARCHITECTURE

Describe:
- Overall architecture
- Frontend architecture
- Backend architecture
- Database architecture
- API architecture
- Component hierarchy
- Service layer
- State management
- Authentication
- External integrations
- Configuration

Include an ASCII architecture diagram based on the repository.

# 6. DATA FLOW

Trace major workflows.

For each workflow show:

User/Input
→ Component/Page
→ State/Hook
→ Service
→ API
→ Backend
→ Database/External Service
→ Response
→ UI

Use actual filenames, functions, routes, and components.

# 7. FEATURE → FILE MAP

Create:

| Feature | UI | Logic | API | Database | Key Files | Status |
|---------|----|-------|-----|----------|-----------|--------|

# 8. ROUTES / PAGES / SCREENS

Document:
- Route
- File
- Purpose
- Components
- Data requirements
- API calls
- Authentication
- Navigation
- Status

# 9. API INVENTORY

If APIs exist:

| Method | Endpoint | Purpose | Request | Response | Implementation File | Auth |
|--------|----------|---------|---------|----------|----------------------|------|

Trace: endpoint → handler/controller → service → database.

# 10. DATABASE / DATA MODEL

Document:
- Database technology
- Tables/collections
- Models/schemas
- Important fields
- Relationships
- Keys
- Indexes
- Validation
- CRUD logic
- Migrations
- Seed data

Include relationship diagram if useful.

# 11. IMPORTANT CODE UNITS

Identify key:
- functions
- classes
- components
- hooks
- services
- controllers
- repositories
- utilities

For each explain:
- Location
- Purpose
- Inputs
- Outputs
- Called by
- Calls
- Why it matters

# 12. DEPENDENCY MAP

Explain major dependencies between modules:
- shared modules
- common utilities
- global state
- tightly coupled modules
- circular dependencies
- cross-layer dependencies

# 13. CONFIGURATION

Inspect:
- .env / .env.example
- config files
- package configuration
- TypeScript config
- build config
- linting
- formatting
- Docker
- CI/CD
- deployment configuration

Never print secret values.

# 14. AUTHENTICATION & SECURITY

If applicable, cover:
- authentication flow
- authorization
- roles
- permissions
- protected routes
- sessions/tokens
- OAuth
- password handling
- input validation
- API security
- environment secrets

Only identify security issues supported by actual code.

# 15. ERROR HANDLING

Explain how the project handles:
- validation errors
- API errors
- database errors
- authentication failures
- network failures
- loading states
- empty states
- exceptions

# 16. TESTING

Identify:
- test framework
- test files
- unit tests
- integration tests
- E2E tests
- coverage
- test commands
- important untested areas

# 17. DEVELOPMENT WORKFLOW

Describe actual commands supported by the repository for:
- install
- setup
- development
- frontend
- backend
- tests
- lint
- type checking
- build
- production

# 18. DEPLOYMENT

Determine:
- deployment platform
- production architecture
- build process
- environment variables
- database deployment
- frontend deployment
- backend deployment
- CI/CD

State clearly if deployment is not implemented.

# 19. IMPLEMENTATION STATUS

Create a table:

| Area | Status | Evidence | Notes |
|------|--------|----------|------|

Use:
- 🟢 Implemented
- 🟡 Partially Implemented
- 🔴 Missing
- ⚪ Placeholder/Unused
- 🔵 Planned

# 20. INCOMPLETE / BROKEN / SUSPICIOUS AREAS

Look for:
- TODO
- FIXME
- broken imports
- missing files
- incomplete features
- dead code
- unused dependencies
- duplicated logic
- inconsistent naming
- placeholder data
- hardcoded values
- type mismatches
- missing error handling

For each, document:
- Location
- Finding
- Evidence
- Impact
- Severity

# 21. TECHNICAL DEBT

Categorize technical debt as:
- HIGH
- MEDIUM
- LOW

Only report debt supported by actual repository evidence.

# 22. SCALABILITY ANALYSIS

Analyze behavior under:
- growing users
- growing data
- increasing API traffic
- growing feature set
- larger development team

Identify bottlenecks and scaling risks.

# 23. HOW TO MODIFY THE PROJECT

Provide a practical modification map:

- UI → files
- Business logic → files
- Database → files
- API → files
- Authentication → files
- Routing → files
- Configuration → files
- Deployment → files

# 24. NEW DEVELOPER ONBOARDING

Give the recommended reading order for a developer who has never seen the repository.

Example:
1. README
2. package configuration
3. app entry point
4. routing
5. main layout
6. state
7. components
8. services
9. APIs
10. database
11. deployment

Adapt to the actual project.

# 25. MASTER MENTAL MODEL

Explain the project in the simplest useful mental model.

Start with:
"Think of this project as..."

Then explain:
- core idea
- architecture
- major layers
- data flow
- key files
- entry points
- important dependencies

# 26. MASTER PROJECT MAP

Create:

PROJECT
│
├── PURPOSE
│
├── FRONTEND
│   ├── ...
│
├── BACKEND
│   ├── ...
│
├── DATABASE
│   ├── ...
│
├── SERVICES
│   ├── ...
│
├── CONFIGURATION
│   ├── ...
│
├── TESTING
│   ├── ...
│
└── DEPLOYMENT
    ├── ...

# 27. FINAL MASTER SUMMARY

Finish with a compact summary:

Project:
Purpose:
Target Users:
Stack:
Architecture:
Frontend:
Backend:
Database:
Authentication:
Main Features:
Main Entry Points:
Important Files:
Main Data Flow:
Current Status:
Incomplete Areas:
Technical Risks:
How to Run:
How to Modify:
Deployment:
Overall Complexity:

## Quality Standard

The output must not read like a generic README summary. It must read like a senior engineer analyzing an inherited codebase and mapping the real system before proposing changes.

The analysis must answer these questions:
1. What is this project?
2. Why does it exist?
3. How does it work?
4. What technologies does it use?
5. What does every important file do?
6. How do the files communicate?
7. Where is every feature implemented?
8. How does data move through the system?
9. Where is data stored?
10. What is actually implemented?
11. What is incomplete?
12. What is unused?
13. What is potentially problematic?
14. How do I run it?
15. How do I modify it?
16. Where should a new developer start?

## Reusability Requirement

This skill must work across different project types and stacks, including:
- React
- Next.js
- Vite
- Node.js
- Express
- FastAPI
- Python
- Java
- Spring Boot
- C/C++
- MERN
- full-stack apps
- CLI tools
- desktop apps
- APIs
- monorepos
- multi-service systems

## Default Behavior

When invoked, the agent should:

1. Inspect the repository before drawing conclusions.
2. Prefer real code evidence over docs.
3. Map file responsibilities, architecture, flows, and risks.
4. Label implementation status clearly.
5. Highlight gaps, incompleteness, and uncertainty.
6. Produce a reproducible map a developer can follow and modify.

## Prompting Pattern for Reuse

Use prompts like:
- "Analyze this repository and produce a master codebase map."
- "Give me the actual architecture and implementation status of this project."
- "Map the feature-to-file relationships and explain how data flows through the system."
- "What is implemented, what is missing, and how should I modify this project?"
- "Produce a senior-engineer codebase summary based on repository evidence only."

## Final Goal

The result should be a reusable, evidence-driven repository analysis workflow that produces a developer-ready master map for understanding, modifying, and extending a codebase safely.
