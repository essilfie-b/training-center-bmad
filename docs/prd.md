# Training Center Management System (TCMS) Product Requirements Document (PRD)

**Version:** 1.0
**Date:** 2025-10-23
**Project:** Training Center Management System (TCMS)
**Prepared By:** PM Agent (John)

---

## Goals

- Reduce trainer assessment creation time by 80% (from ~30 hours to ~6 hours per module) through AI-powered question generation
- Decrease lab grading turnaround from 2-3 days to <24 hours through queue management, standardized rubrics, and streamlined workflows
- Ensure 100% of employment decisions are supported by documented performance data with complete audit trails
- Scale training operations to support 150+ trainees per cohort (50% growth) without requiring additional training staff
- Launch MVP operational system in time for Q1 2026 NSP cohort intake (6-month delivery timeline)
- Provide real-time visibility into trainee progress, performance metrics, and at-risk identification for all training staff roles
- Establish centralized, structured curriculum management replacing fragmented Microsoft Loop documents
- Enable self-paced learning with deadline accountability, supporting ~100 trainees annually across 6 technical specializations

## Background Context

The company's training center operates two primary programs—Graduate Training Program (GTP, 6 months) and National Service Personnel Training (NSP, 12 months)—serving approximately 100+ trainees annually across six technical specializations (Backend, Frontend, QA, UI/UX, Data Engineering, DevOps). Currently, training operations rely on fragmented manual processes: course materials are scattered across Microsoft Loop with no progress tracking, trainers manually create hundreds of assessment questions per cohort (consuming 20-30 hours per module), TAs manually grade ~100 lab submissions with inconsistent rubrics and 2-3 day turnaround times, and employment decisions are made using performance data scattered across spreadsheets without audit trails or standardized criteria.

TCMS addresses these pain points by providing a unified platform that manages the complete training lifecycle—from content delivery and AI-powered assessment generation to lab grading workflows and data-driven employment decision support. The system eliminates administrative burden on training staff, provides trainees with clear expectations and timely feedback, and ensures fair, defensible employment decisions backed by comprehensive performance analytics. The MVP must be operational for the Q1 2026 cohort intake, making the 6-month timeline a critical business constraint.

## Change Log

| Date | Version | Description | Author |
|------|---------|-------------|--------|
| 2025-10-23 | 1.0 | Initial PRD creation from approved Project Brief | PM Agent (John) |

---

## Requirements

### Functional

#### Authentication & User Management

- **FR1:** The system shall authenticate users via email and password credentials stored securely with bcrypt hashing (minimum 10 rounds)
- **FR2:** The system shall generate temporary passwords when Head of Training Center creates user accounts and send credentials via email
- **FR3:** The system shall force users to reset their password upon first login before accessing any other system functionality
- **FR4:** The system shall enforce password requirements: minimum 8 characters, at least one uppercase letter, one lowercase letter, one number, and one special character
- **FR5:** The system shall lock user accounts after 5 consecutive failed login attempts for 15 minutes
- **FR6:** The system shall provide "Forgot Password" functionality with email-based password reset links valid for 1 hour
- **FR7:** The system shall support five distinct role types: Trainee, TA, Head of Specialization, Head of Program, Head of Training Center
- **FR8:** The system shall enforce workspace-based data isolation ensuring users can only access data within their assigned workspace
- **FR9:** The system shall allow Head of Training Center to create and manage multiple workspaces with independent data structures
- **FR10:** The system shall provide a user provisioning interface accessible only to Head of Training Center for creating all user accounts

#### Workspace & Organizational Structure

- **FR11:** The system shall support workspace creation by Head of Training Center with configurable programs (GTP, NSP, or both)
- **FR12:** The system shall support seven specializations per workspace: Frontend, Backend, UI/UX, Data Engineering, Quality Assurance, DevOps, Cybersecurity
- **FR13:** The system shall maintain curriculum hierarchy: Workspace → Program (GTP/NSP) → Cohort → Specialization → Module → Topic
- **FR14:** The system shall allow Head of Training Center to assign Head of Program users with specific program categories (GTP or NSP) within a workspace
- **FR15:** The system shall allow Head of Training Center to assign Head of Specialization users with specific specialization categories (Frontend, Backend, UI/UX, Data Engineering, Quality Assurance, DevOps, Cybersecurity) within a workspace
- **FR16:** The system shall allow Head of Training Center to assign TAs to specific Head of Specialization within a workspace
- **FR17:** The system shall restrict users to a single workspace assignment (except Head of Training Center who has global access)
- **FR18:** The system shall enforce one Head of Program per program (GTP or NSP) per workspace
- **FR19:** The system shall support bulk content import from Microsoft Loop as a one-time migration activity per workspace

#### Content Management

- **FR20:** The system shall provide rich text editing capabilities for topic content creation and modification by TAs within their assigned specializations
- **FR21:** The system shall publish content changes immediately upon save with no approval workflow required
- **FR22:** The system shall track complete version history of all content changes with rollback capability for safety
- **FR23:** The system shall support upload of content assets including PDFs, videos, code samples, and external links

#### Self-Paced Learning & Progress Tracking

- **FR24:** The system shall allow trainees to browse and access all modules and topics within their assigned specialization without forced sequencing
- **FR25:** The system shall track progress at topic level with states: not started, in progress, completed
- **FR26:** The system shall define topic completion as passing both Knowledge Check (KC) and Module Assessment (MA)
- **FR27:** The system shall define module completion as completing all topics plus submitting the module lab
- **FR28:** The system shall enforce module deadline tracking, recording on-time versus late completion status

#### AI-Powered Assessment Generation

- **FR29:** The system shall generate Knowledge Checks with 30+ moderate-to-hard difficulty questions per topic using AI (Claude/GPT-4)
- **FR30:** The system shall generate Module Assessments with 30+ very hard difficulty questions per topic using AI
- **FR31:** The system shall support question types: single-answer MCQ, multi-select MCQ, and coding analysis MCQ
- **FR32:** The system shall maintain question pools with randomized subset presentation to prevent memorization
- **FR33:** The system shall auto-publish AI-generated Knowledge Checks (Yolo mode) and require TA review for Module Assessments (Safe mode)
- **FR34:** The system shall provide TA controls to view, edit, approve, regenerate, and reject AI-generated questions
- **FR35:** The system shall flag questions with <30% or >90% success rates for TA review via question performance analytics
- **FR35a:** The system shall provide trainers with selectable assessment generation criteria including: difficulty level, question types, number of questions, cognitive level (Bloom's Taxonomy), focus areas, question distribution, and scenario-based options
- **FR35b:** The system shall allow trainers to save generation criteria as reusable presets for consistent assessment creation across topics

#### Assessment Taking & Scoring

- **FR36:** The system shall allow trainees 3 attempts for Knowledge Checks and 2 attempts for Module Assessments (configurable per assessment)
- **FR37:** The system shall prevent retaking assessments after passing—once a trainee passes, the score is final
- **FR38:** The system shall auto-grade all MCQ questions and provide immediate score feedback after each attempt
- **FR39:** The system shall display correct answers only after all attempts are exhausted
- **FR40:** The system shall display complete attempt history to trainees for all assessments

#### Lab Submission & Grading

- **FR41:** The system shall accept lab submissions as GitHub repository links (primary method) with validation of link accessibility
- **FR42:** The system shall accept lab submissions as file uploads (secondary method) supporting code files, documents, and zip archives
- **FR43:** The system shall archive repository state at submission time to prevent post-submission changes
- **FR44:** The system shall require GitHub repositories to be public for lab submissions
- **FR45:** The system shall enforce final submission confirmation with no resubmission capability
- **FR46:** The system shall assign TAs to specific mentees based on specialization in a mentor-mentee relationship model
- **FR47:** The system shall restrict TAs to grading only their assigned mentees' labs
- **FR48:** The system shall provide rubric-based grading interface for TAs with standardized evaluation criteria
- **FR49:** The system shall require text feedback field completion before TAs can submit lab grades
- **FR50:** The system shall send email notifications to trainees when their labs are graded

#### Dashboards & Analytics

- **FR51:** The system shall display trainee dashboard showing current workspace, program, specialization, cohort, progress visualization (completed topics/modules, percentage completion), upcoming deadlines, recent scores, and on-time submission status
- **FR52:** The system shall provide recommended next steps on trainee dashboard (e.g., "Complete Module 3 Lab by Oct 30")
- **FR53:** The system shall provide TA dashboard displaying assigned mentees list, pending lab submissions from mentees, mentee progress summaries, and content editing tools for assigned specialization
- **FR54:** The system shall provide Head of Specialization dashboard with specialization-wide analytics (topic difficulty analysis, TA assignments, question approval queue) within their workspace
- **FR55:** The system shall provide Head of Program dashboard with program-specific cohort performance overview (completion rates, average scores by specialization, at-risk trainees) within their workspace
- **FR56:** The system shall provide Head of Training Center dashboard with multi-workspace analytics, workspace management, user management across all workspaces, and system-wide configuration

#### Performance Metrics & Employment Decisions

- **FR57:** The system shall auto-calculate trainee performance metrics: KC average, MA average, Lab average, Overall technical score (weighted), Completion rate, On-time submission rate, Improvement trend
- **FR58:** The system shall store monthly performance snapshots for complete audit trail within each workspace
- **FR59:** The system shall support configurable evaluation thresholds per workspace, program, and specialization (minimum KC %, MA %, Lab %, completion %, on-time %)
- **FR60:** The system shall restrict threshold configuration permissions to Heads of Program and Head of Training Center only
- **FR61:** The system shall provide red flag alerts for trainees falling below configured thresholds
- **FR62:** The system shall support three-level employment review workflow: Head of Specialization adds notes → Head of Program makes recommendation → Head of Training Center makes final decision
- **FR63:** The system shall support manual soft skills score input tracked separately from technical scores
- **FR64:** The system shall generate employment decision export reports in PDF and Excel formats per workspace

#### Notifications & Communication

- **FR65:** The system shall send email notifications for: account creation with temporary credentials, password reset requests, upcoming deadlines (3 days, 1 day before), missed deadlines, lab graded, new announcements
- **FR66:** The system shall support in-platform announcements at Workspace-wide, Program-wide, Cohort-wide, and Specialization-wide levels
- **FR67:** The system shall allow trainees to configure notification preferences (toggle email notifications)

#### Admin & System Configuration

- **FR68:** The system shall enable Head of Training Center to create and manage workspaces
- **FR69:** The system shall enable Head of Training Center to create programs (GTP, NSP, or both) within workspaces
- **FR70:** The system shall enable Head of Training Center to create and manage seven specializations (Frontend, Backend, UI/UX, Data Engineering, Quality Assurance, DevOps, Cybersecurity) per workspace
- **FR71:** The system shall enable Head of Training Center to create modules and topics within specializations
- **FR72:** The system shall enable Head of Training Center to enroll trainees into workspace, program, cohort, and specialization combinations
- **FR73:** The system shall enable Head of Training Center to assign TAs to Head of Specialization within workspaces
- **FR74:** The system shall support TA-to-mentee assignment for establishing mentorship relationships
- **FR75:** The system shall allow configuration of module deadlines per cohort per workspace
- **FR76:** The system shall allow configuration of assessment attempt limits per workspace (default: KC=3, MA=2, Lab=1)
- **FR77:** The system shall maintain comprehensive audit logs for: user actions, grade changes, employment decisions, content changes, threshold modifications, workspace operations

### Non Functional

- **NFR1:** The system shall achieve 99.5% uptime during business hours (8am-8pm WAT)
- **NFR2:** The system shall load pages in <3 seconds on 4G connections
- **NFR3:** The system shall respond to assessment submissions in <1 second
- **NFR4:** The system shall support 100+ concurrent users without performance degradation
- **NFR5:** The system shall support file uploads up to 50MB for lab submissions
- **NFR6:** The system shall comply with WCAG 2.1 AA accessibility standards including keyboard navigation and screen reader support
- **NFR7:** The system shall support latest 2 versions of Chrome, Firefox, Safari, and Edge browsers (IE not supported)
- **NFR8:** The system shall encrypt all data in transit using TLS 1.3
- **NFR9:** The system shall encrypt all data at rest using AES-256 encryption
- **NFR10:** The system shall implement daily automated backups with 30-day retention
- **NFR11:** The system shall achieve Recovery Time Objective (RTO) of <4 hours for critical system failures
- **NFR12:** The system shall enforce workspace-level data isolation—users can only access data within their assigned workspace (except Head of Training Center)
- **NFR12a:** The system shall prevent cross-cohort data leakage—trainee performance data visible only to authorized roles within the same workspace
- **NFR13:** The system shall log all grade changes, employment decisions, and admin actions with timestamp and user ID for audit compliance
- **NFR14:** The system shall handle AI API rate limits gracefully with appropriate user feedback during question generation
- **NFR15:** The system shall optimize infrastructure costs to stay within estimated $500-1000/month operational budget for 100 trainees

---

## User Interface Design Goals

### Overall UX Vision

TCMS will deliver a **workspace-aware, role-tailored, dashboard-centric experience** that reduces cognitive load through clear information hierarchy and contextual navigation. Each user role sees only relevant functionality upon login—trainees focus on learning progress and deadlines within their workspace, TAs see grading queues and mentee status for their assigned specialization, and Heads access analytics dashboards scoped to their workspace and responsibilities. The Head of Training Center has a unique cross-workspace view for system-wide management. The design prioritizes **speed and efficiency** for repetitive tasks (grading, content editing) while providing **guided workflows** for complex processes (workspace creation, user provisioning, employment decisions, question review). Self-service is paramount: trainees track their own progress without asking staff, and staff access real-time data without generating reports.

### Key Interaction Paradigms

- **Dashboard-First Navigation:** Users land on role-specific dashboards serving as primary navigation hubs with quick-access cards for top tasks
- **Progressive Disclosure:** Complex workflows (employment review, AI question approval) reveal details progressively to avoid overwhelming users
- **Inline Editing:** Content updates and question edits occur in-place without full page refreshes for trainer efficiency
- **Notification Center:** Centralized in-app notification panel augmenting email alerts for trainees and staff
- **Bulk Actions:** TAs and trainers can perform batch operations (approve multiple questions, update multiple deadlines) where appropriate
- **Search-First for Large Lists:** Global search and filtering for trainee lists, question banks, and content libraries

### Core Screens and Views

- **Login & First-Time Password Reset:** Email/password login form with "Forgot Password" link; first-time users automatically redirected to mandatory password reset page with validation feedback
- **Trainee Dashboard:** Workspace-aware central hub showing assigned workspace/program/specialization, progress rings (module completion %), upcoming deadlines timeline, recent assessment scores, recommended next actions, and quick links to continue learning
- **Learning View (Trainee):** Topic content display with embedded rich media, sidebar showing module structure, progress indicators, and "Take Assessment" CTAs when ready
- **Assessment Taking Interface:** Clean, distraction-free environment with question counter, timer (if applicable), review/flagging capability, and submit confirmation
- **TA Dashboard:** Overview of assigned mentees (filtered by specialization), pending lab submissions queue, content editing shortcuts, and question review tasks
- **TA Grading Queue:** Card-based layout of pending lab submissions with mentee info, lab title, submission date, and one-click access to grading interface
- **Lab Grading Interface:** Split view showing lab requirements/rubric (left), submitted code/files (right), inline commenting, rubric scoring checkboxes, overall grade input, and feedback textarea
- **TA Question Review:** List/grid of AI-generated questions with difficulty/type filters, preview modal for each question, approve/edit/regenerate/reject actions
- **Content Editor:** Rich WYSIWYG editor for topic content with asset upload, preview, version history sidebar, and immediate publish
- **Head of Specialization Dashboard:** Specialization-scoped analytics within assigned workspace showing topic difficulty, TA performance, question approval queue, and trainee progress by specialization
- **Head of Program Dashboard:** Program-scoped analytics within assigned workspace (GTP or NSP) showing cohort performance, completion rates, average scores by specialization, at-risk trainees, and employment readiness
- **Head of Training Center Dashboard:** Multi-workspace overview with workspace selector, system-wide analytics, workspace management controls, cross-workspace user management, and global configuration
- **Workspace Management (Head of Training Center):** Interface for creating/editing workspaces, configuring programs (GTP, NSP, both), managing specializations, and viewing workspace-level statistics
- **User Management (Head of Training Center):** Tabular user list with filters by workspace/role/specialization, inline role assignment, bulk enrollment tools, TA-mentee assignment interface, and new user creation with automatic credential email
- **Employment Decision Workflow:** Stepper interface showing three-level review process (Head of Specialization → Head of Program → Head of Training Center), trainee performance summary card, manual notes input at each level, and final decision submission with confirmation
- **System Configuration (Head of Training Center):** Form-based interfaces for threshold configuration per workspace/program/specialization, deadline setting, assessment attempt limits, with clear permission indicators

### Accessibility: WCAG 2.1 AA

The system must meet WCAG 2.1 Level AA compliance to ensure usability for all training staff and trainees, including those with disabilities. This includes full keyboard navigation support (no mouse-only interactions), screen reader compatibility with proper ARIA labels, sufficient color contrast ratios (4.5:1 for text), focus indicators on all interactive elements, and alternative text for all images and visual content.

### Branding

The system should feature a professional, clean, modern design language appropriate for enterprise training management. UI component libraries like Material-UI, Ant Design, or Chakra UI are recommended for rapid development and accessibility compliance. Color palette should prioritize readability and accessibility over flashy branding. The platform should feel like a productivity tool, not a gamified learning app. Workspace branding (logos, colors) may be considered in future phases but is out of scope for MVP.

### Target Device and Platforms: Web Responsive

MVP targets **web-responsive design** for desktop and tablet experiences (no native mobile apps). The platform must function on desktop computers (primary use case for content editing, lab grading, analytics) and tablets (trainee learning, content review). Mobile phone layouts are not prioritized for MVP but should gracefully degrade. Minimum viewport support: 768px width (tablet portrait) to 1920px+ (desktop). Phase 2 will introduce React Native mobile apps for iOS and Android.

---

## Technical Assumptions

### Repository Structure: Monorepo

The project will utilize a **monorepo architecture** using a tool like Turborepo or Nx to manage frontend, backend, and shared code in a single repository. This approach enables:
- Shared TypeScript types between frontend and backend for type safety across API boundaries
- Atomic commits affecting both client and server code
- Unified versioning and dependency management
- Simplified CI/CD pipelines with a single build/test/deploy workflow

**Rationale:** For an MVP with a small team (3-4 developers), a monorepo reduces coordination overhead, ensures consistency, and accelerates development. The codebase is not yet large enough to justify splitting into separate repositories, and maintaining a single source of truth simplifies onboarding and refactoring.

### Service Architecture

**MVP Approach: Monolithic Backend with Modular Structure**

The backend will be built as a **monolithic application** with clear internal module boundaries that can be extracted into microservices post-MVP if needed. Key modules include:
- **Authentication Module** (email/password authentication, password reset, session management)
- **Workspace Management Module** (workspace isolation, multi-tenancy support)
- **Content Management Module** (topics, modules, versioning)
- **Assessment Module** (question generation, taking, grading)
- **Lab Management Module** (submissions, TA grading)
- **Analytics & Reporting Module** (performance metrics, dashboards)
- **Notification Module** (email, in-app alerts)
- **Admin Module** (user management, configuration)

**Rationale:** A monolith accelerates MVP development by avoiding distributed system complexity (inter-service communication, eventual consistency, service discovery). The 6-month timeline and 100-user scale do not justify microservices overhead. However, modular code structure prepares for future decomposition if scale demands it (e.g., AI service, notification service could be split in Phase 2).

**Technology Stack:**
- **Backend Framework:** Node.js with Express (preferred) or Python with FastAPI
  - Node.js chosen for team familiarity, TypeScript consistency with frontend, and rich ecosystem for authentication libraries
- **API Style:** RESTful API for CRUD operations; consider GraphQL for complex dashboard queries if needed
- **Background Jobs:** Bull (Node.js) or Celery (Python) for AI question generation, email notifications, and analytics aggregation

### Testing Requirements

**MVP Testing Strategy: Unit + Integration with Manual E2E for Critical Paths**

Testing requirements balance quality assurance with MVP speed constraints:

1. **Unit Testing (Required):**
   - Backend: 70%+ code coverage for business logic (assessment scoring, performance calculations, access control)
   - Frontend: Unit tests for critical utilities and complex components (assessment timer, rubric calculator)
   - Test framework: Jest (JavaScript/TypeScript) or pytest (Python)

2. **Integration Testing (Required):**
   - API integration tests for all major endpoints using supertest or similar
   - Database integration tests ensuring CRUD operations work correctly
   - Authentication flow integration tests (login, password reset, first-time password change)
   - Workspace isolation integration tests ensuring data cannot leak across workspaces
   - AI API integration test with mocked responses for predictable testing

3. **End-to-End Testing (Manual for MVP):**
   - Manual QA test scripts for critical user journeys: trainee takes assessment, TA grades lab, trainer approves questions, Head makes employment decision
   - Automated E2E tests deferred to post-MVP (Playwright/Cypress)—manual QA faster for 6-month timeline
   - UAT (User Acceptance Testing) with 5-10 training staff and trainees from pilot cohort

4. **Load/Performance Testing (Pre-Launch):**
   - Load test with 100+ concurrent users simulating peak assessment periods
   - Tools: k6 or Apache JMeter
   - Target: <3 second page loads, <1 second API responses under load

5. **Local Testability:**
   - CLI commands for seeding test data (users, content, assessments) for rapid developer testing
   - Docker Compose setup for local development with PostgreSQL and Redis
   - All backend modules must be testable without full system deployment

**Rationale:** Full test automation would delay MVP launch. Prioritizing unit and integration tests provides safety net for regression while manual E2E testing covers critical paths. Post-MVP, invest in automated E2E suite as system stabilizes.

### Additional Technical Assumptions and Requests

- **Frontend Framework:** React with TypeScript, state management via Redux Toolkit or Zustand, UI component library using Material-UI (MUI), Ant Design, or Chakra UI for rapid development and accessibility
- **Rich Text Editor:** Quill or TipTap for content authoring with support for embedded media
- **Database:** PostgreSQL as primary relational database with JSONB support for flexible question storage and workspace-level data isolation; Redis for caching session data and performance metrics
- **Multi-Tenancy Strategy:** Schema-per-workspace or row-level security (RLS) with workspace_id foreign keys on all data tables to ensure complete data isolation between workspaces
- **File Storage:** Cloud object storage (AWS S3, Azure Blob Storage, or Google Cloud Storage) for lab submissions, content assets (videos, PDFs), and repository snapshots
- **AI/ML Integration:** OpenAI GPT-4 or Anthropic Claude API for question generation; consider cost optimization strategies for AI API usage at scale
- **Hosting/Infrastructure:** Cloud provider (AWS, Azure, or GCP) with managed services for compute, database, and storage; GitHub Actions or GitLab CI for CI/CD
- **Monitoring & Logging:** Application monitoring service (Datadog, New Relic, or cloud-native solutions) for performance monitoring, Sentry for error tracking and alerting
- **Email Service:** Transactional email service (SendGrid, AWS SES, Mailgun, or Postmark) for account credentials, password resets, and notifications
- **Security:** Email/password authentication with bcrypt hashing, password reset tokens, session management with HttpOnly cookies or JWT, TLS 1.3 for data in transit, AES-256 for data at rest, RBAC and workspace isolation enforced at API layer
- **Compliance:** Verify data residency requirements for Nigeria/West Africa; ensure audit logging meets company policies for employment decision data retention; implement GDPR-compliant user data handling if applicable
- **Development Environment:** Docker Compose for local dev environment with PostgreSQL and Redis, Git for version control with feature branch workflow, pull request reviews required before merging to main
- **Code Quality:** ESLint + Prettier for JavaScript/TypeScript, pre-commit hooks for linting and formatting, code review required for all changes
- **Documentation:** OpenAPI/Swagger for API documentation auto-generated from code, inline code comments for complex business logic, README for setup instructions

---

## Epic List

The TCMS MVP is structured into **8 epics** that deliver the system incrementally, following agile best practices. Each epic represents a significant, end-to-end, deployable increment of functionality:

1. **Epic 1: Foundation & Authentication Infrastructure** - Establish project scaffolding, email/password authentication with temporary password flow, password reset functionality, basic user management, workspace isolation, and deployment pipeline with a simple health check endpoint to validate the full stack is operational

2. **Epic 2: Workspace Management & Multi-Tenancy** - Implement workspace creation, management, and data isolation with workspace-scoped user assignments and program configuration (GTP, NSP, or both)

3. **Epic 3: Content Management & Curriculum Structure** - Build content creation, editing, and organization capabilities allowing TAs to migrate and manage training materials within the hierarchical curriculum structure (Workspace → Program → Cohort → Specialization → Module → Topic)

4. **Epic 4: Self-Paced Learning & Progress Tracking** - Enable trainees to browse content, track progress, and view their learning dashboard with deadline visibility and completion status within their assigned workspace

5. **Epic 5: AI-Powered Assessment Generation & Management** - Implement AI question generation for Knowledge Checks and Module Assessments with TA review workflows and question pool management

6. **Epic 6: Assessment Taking & Auto-Grading** - Enable trainees to take randomized assessments with attempt limits, auto-grading, and immediate feedback

7. **Epic 7: Lab Submission & TA Grading Workflow** - Build lab assignment creation, trainee submission (GitHub links and file uploads), TA-mentee assignment, rubric-based grading interface, and feedback delivery

8. **Epic 8: Analytics, Performance Metrics & Employment Decisions** - Implement performance calculation, workspace-aware Head dashboards, configurable thresholds per workspace/program/specialization, at-risk alerts, and three-level employment review workflow (Head of Specialization → Head of Program → Head of Training Center) with audit trails

**Rationale for Epic Structure:**
- **Epic 1 delivers infrastructure + authentication** with temporary password flow and workspace isolation foundation to establish CI/CD and validate full-stack deployment early
- **Epic 2 delivers workspace multi-tenancy** as a critical architectural foundation that all subsequent features depend on
- **Epics 3-4 deliver trainee-facing value** (content access and learning) enabling partial system use even before assessments are ready
- **Epics 5-6 deliver assessment capability** end-to-end (generation → taking → grading)
- **Epic 7 delivers lab workflows** which are complex enough to warrant a dedicated epic and can function independently of assessments
- **Epic 8 delivers decision-making tools** for leadership, completing the employment lifecycle—deferred to end since it depends on accumulated performance data

Each epic builds upon previous epics' functionality without requiring future work, ensuring deployable increments throughout development.

---

## Epic 1: Foundation & Authentication Infrastructure

**Goal:** Establish the foundational technical infrastructure for TCMS including project scaffolding, Microsoft SSO authentication, basic role-based access control, user management capabilities, and continuous deployment pipeline. This epic delivers a working system with health check endpoint and admin ability to provision the first users, validating the full technology stack and deployment process before building complex features.

### Story 1.1: Project Initialization & Repository Setup

**As a** developer,
**I want** the project repository initialized with frontend, backend, shared types, and development environment configuration,
**so that** the team can begin development with consistent tooling and structure.

**Acceptance Criteria:**

1. Monorepo initialized using Turborepo or Nx with workspaces for frontend (`apps/web`), backend (`apps/api`), and shared code (`packages/types`, `packages/utils`)
2. Backend workspace configured with Node.js + Express + TypeScript, including tsconfig, ESLint, Prettier, and Jest test setup
3. Frontend workspace configured with React + TypeScript + Vite (or Create React App), including tsconfig, ESLint, Prettier, and Jest + React Testing Library setup
4. Shared `packages/types` workspace exports common TypeScript interfaces (e.g., `User`, `Role`) imported by both frontend and backend
5. Docker Compose file created defining PostgreSQL and Redis services for local development
6. README.md documents setup instructions: clone repo, install dependencies (`npm install`), start services (`docker-compose up`), run dev servers
7. Git repository created with `.gitignore` excluding `node_modules`, `.env`, and build artifacts
8. Pre-commit hooks configured using Husky to run ESLint and Prettier on staged files
9. Local development confirmed: `npm run dev` starts both frontend and backend with hot reload

### Story 1.2: Database Schema Foundation & Migrations

**As a** developer,
**I want** the initial database schema created with migration tooling,
**so that** user authentication and role management data can be persisted.

**Acceptance Criteria:**

1. Database migration tool configured (Prisma, TypeORM, or Knex) with migrations folder
2. Initial migration created defining `users` table with columns: id (UUID primary key), email (unique), display_name, role (enum: Trainee, TA, Trainer, HeadOfChapter, HeadOfProgram, HeadOfTrainingCenter), azure_ad_id (unique), created_at, updated_at
3. `specializations` table created with columns: id (UUID), name (Backend, Frontend, QA, UIUX, DataEngineering, DevOps), created_at
4. `user_specialization_assignments` junction table created with columns: id (UUID), user_id (FK to users), specialization_id (FK to specializations), assignment_type (enum: Trainer, TA, Trainee), created_at
5. Migration can be run via CLI command (e.g., `npm run migrate:up`) to apply schema changes to local PostgreSQL
6. Migration rollback command available (e.g., `npm run migrate:down`)
7. Database seeding script created to insert 6 specializations (Backend, Frontend, QA, UI/UX, Data Engineering, DevOps)
8. Local testability: Developer can run `npm run db:reset` to drop schema, re-run migrations, and seed data for clean state

### Story 1.3: Microsoft SSO Authentication Integration

**As a** user of any role,
**I want** to log in using my company Microsoft account,
**so that** I can securely access TCMS without managing additional passwords.

**Acceptance Criteria:**

1. Azure AD application registered in company Azure tenant with redirect URIs for local development (`http://localhost:3000/auth/callback`) and production (TBD)
2. Backend implements OAuth 2.0 authorization code flow using `passport-azure-ad` or `@azure/msal-node` library
3. Backend exposes `/auth/login` endpoint redirecting users to Microsoft login page
4. Backend exposes `/auth/callback` endpoint handling OAuth callback, exchanging authorization code for access token, and extracting user email and Azure AD ID
5. Upon successful authentication, backend queries `users` table by `azure_ad_id`; if user exists, create session; if not, return error "User not provisioned"
6. Sessions stored in Redis with 24-hour expiry using `express-session` with Redis store
7. Backend exposes `/auth/me` endpoint returning authenticated user's profile (id, email, display_name, role) or 401 if not authenticated
8. Frontend implements login page with "Sign in with Microsoft" button calling `/auth/login`
9. Frontend implements authentication state management storing user profile and handling session expiry (redirect to login)
10. Frontend protects all routes except login page with authentication check; unauthenticated users redirected to login
11. Local testability: Developer can configure Azure AD test account and successfully authenticate in local environment

### Story 1.4: Role-Based Access Control (RBAC) Middleware

**As a** developer,
**I want** API endpoints protected by role-based access control,
**so that** users can only access functionality appropriate to their assigned role.

**Acceptance Criteria:**

1. Backend implements authentication middleware (`requireAuth`) checking session validity; returns 401 if not authenticated
2. Backend implements authorization middleware (`requireRole(allowedRoles)`) checking if authenticated user's role is in allowedRoles array; returns 403 if unauthorized
3. Backend implements specialization-scoped authorization middleware (`requireSpecialization(scopeCheck)`) verifying user has assignment to requested specialization; returns 403 if unauthorized
4. All protected API endpoints use `requireAuth` middleware as first middleware in chain
5. Role-restricted endpoints (e.g., admin user management) use `requireRole(['HeadOfTrainingCenter'])` middleware
6. Unit tests created for authentication and authorization middleware with mocked sessions covering: authenticated user passes, unauthenticated user receives 401, wrong role receives 403, correct role passes
7. Local testability: Developer can seed test users with different roles and verify access control via API requests (Postman/curl)

### Story 1.5: User Management Interface for Head of Training Center

**As a** Head of Training Center,
**I want** to provision new users and assign them roles and specializations,
**so that** training staff and trainees can access the system.

**Acceptance Criteria:**

1. Backend exposes `POST /api/admin/users` endpoint (requires HeadOfTrainingCenter role) accepting: email, display_name, role, specialization_ids[] (if applicable)
2. Endpoint validates email format and checks for duplicate email; returns 400 if invalid or duplicate
3. Endpoint inserts user into `users` table with provided details (azure_ad_id initially null until first login)
4. Endpoint inserts records into `user_specialization_assignments` for each specialization_id if provided
5. Endpoint returns created user object (id, email, display_name, role, specializations)
6. Backend exposes `GET /api/admin/users` endpoint (requires HeadOfTrainingCenter role) returning paginated list of all users with filters: role, specialization
7. Backend exposes `PATCH /api/admin/users/:id` endpoint (requires HeadOfTrainingCenter role) allowing updates to display_name, role, and specialization assignments
8. Backend exposes `DELETE /api/admin/users/:id` endpoint (requires HeadOfTrainingCenter role) soft-deleting user (set deleted_at timestamp)
9. Frontend implements User Management page (route: `/admin/users`) accessible only to HeadOfTrainingCenter role showing tabular user list with columns: name, email, role, specializations, actions (edit, delete)
10. Frontend implements "Add User" modal with form fields: email (required), display name (required), role (dropdown, required), specializations (multi-select, conditional on role)
11. Frontend implements "Edit User" modal pre-populated with existing user data allowing modifications
12. Frontend implements bulk enrollment interface allowing CSV upload with columns: email, display_name, role, specialization1, specialization2 (for batch trainee onboarding)
13. Local testability: Admin user can provision a test trainee, trainer, and TA via UI and verify they appear in user list

### Story 1.6: Health Check & System Status Endpoint

**As a** developer or DevOps engineer,
**I want** a health check endpoint indicating system operational status,
**so that** monitoring tools and load balancers can verify the application is running correctly.

**Acceptance Criteria:**

1. Backend exposes `GET /health` endpoint (no authentication required) returning 200 OK with JSON: `{"status": "healthy", "timestamp": "<ISO 8601>", "version": "<version>"}`
2. Endpoint checks PostgreSQL connection by executing simple query (`SELECT 1`); if database unreachable, return 503 Service Unavailable with `{"status": "unhealthy", "reason": "database"}`
3. Endpoint checks Redis connection by executing PING command; if Redis unreachable, return 503 with `{"status": "unhealthy", "reason": "cache"}`
4. Frontend root path (`/`) displays simple page with text "TCMS is running" and link to login page (this serves as canary for frontend deployment)
5. CI/CD pipeline configured to call `/health` endpoint after deployment; deployment marked failed if health check returns non-200 status
6. Local testability: Developer can verify health check returns 200 when services running, and 503 when PostgreSQL or Redis stopped

### Story 1.7: CI/CD Pipeline Setup

**As a** developer,
**I want** automated build, test, and deployment pipeline,
**so that** code changes can be continuously integrated and deployed to staging/production environments.

**Acceptance Criteria:**

1. GitHub Actions (or Azure DevOps Pipelines) workflow created with triggers: push to main branch, pull request opened/updated
2. Workflow includes job: "lint" running ESLint and Prettier checks on all workspaces; fails if linting errors detected
3. Workflow includes job: "test" running `npm run test` for backend and frontend; fails if any tests fail
4. Workflow includes job: "build" running `npm run build` for frontend and backend; fails if build errors detected
5. Workflow includes job: "deploy-staging" (runs only on main branch push) deploying backend to Azure App Service staging slot and frontend to Azure Static Web Apps staging environment
6. Deployment job includes post-deploy health check calling `/health` endpoint; rollback if unhealthy
7. Workflow artifacts include build outputs and test coverage reports
8. Pull request status checks configured to require lint, test, and build jobs to pass before merge allowed
9. Local testability: Developer can trigger workflow manually via GitHub Actions UI and observe all jobs passing

---

## Epic 2: Content Management & Curriculum Structure

**Goal:** Enable trainers and TAs to create, organize, and manage training content within a structured curriculum hierarchy (Program → Cohort → Specialization → Module → Topic). This epic delivers content authoring tools with rich text editing, asset uploads, version history, and the ability to migrate existing materials from Microsoft Loop into the TCMS platform.

### Story 2.1: Program & Cohort Data Models and CRUD APIs

**As a** Head of Training Center,
**I want** to create and manage training programs and cohorts,
**so that** I can organize training cycles for GTP and NSP programs.

**Acceptance Criteria:**

1. Database migration creates `programs` table with columns: id (UUID), name (e.g., "Graduate Training Program"), abbreviation (e.g., "GTP"), duration_months (integer), created_at, updated_at
2. Database migration creates `cohorts` table with columns: id (UUID), program_id (FK to programs), name (e.g., "GTP 2026 Q1"), start_date (date), end_date (date, nullable), is_active (boolean), created_at, updated_at
3. Backend exposes `POST /api/admin/programs` endpoint (requires HeadOfTrainingCenter role) creating new program
4. Backend exposes `GET /api/admin/programs` endpoint (requires authenticated user) returning all programs
5. Backend exposes `POST /api/admin/cohorts` endpoint (requires HeadOfTrainingCenter role) creating new cohort linked to program_id
6. Backend exposes `GET /api/admin/cohorts` endpoint (requires authenticated user) returning all cohorts with filters: program_id, is_active
7. Backend exposes `PATCH /api/admin/cohorts/:id` endpoint (requires HeadOfTrainingCenter role) updating cohort details including is_active flag
8. Frontend implements Programs & Cohorts management page (route: `/admin/programs`) showing list of programs, each expandable to show associated cohorts
9. Frontend implements "Create Program" and "Create Cohort" modals with form validation
10. Local testability: Admin creates "GTP" and "NSP" programs, then creates "GTP 2026 Q1" cohort and verifies via API response

### Story 2.2: Module & Topic Data Models and CRUD APIs

**As a** Trainer,
**I want** to create modules and topics within my assigned specialization,
**so that** I can structure the curriculum into logical learning units.

**Acceptance Criteria:**

1. Database migration creates `modules` table with columns: id (UUID), specialization_id (FK to specializations), name (e.g., "Python Basics"), description (text), sequence_order (integer), created_at, updated_at
2. Database migration creates `topics` table with columns: id (UUID), module_id (FK to modules), name (e.g., "Variables and Data Types"), content (text, stores rich text HTML), sequence_order (integer), created_at, updated_at, created_by_user_id (FK to users)
3. Backend exposes `POST /api/modules` endpoint (requires Trainer or Head role with specialization assignment) creating module within assigned specialization
4. Backend exposes `GET /api/modules` endpoint (authenticated users) returning modules filtered by specialization_id with topics count per module
5. Backend exposes `POST /api/topics` endpoint (requires Trainer or TA with specialization assignment) creating topic within module, validating user has access to module's specialization
6. Backend exposes `GET /api/modules/:moduleId/topics` endpoint (authenticated users) returning all topics for a module ordered by sequence_order
7. Backend exposes `PATCH /api/topics/:id` endpoint (requires Trainer or TA with specialization assignment) updating topic name, content, or sequence_order
8. Backend exposes `DELETE /api/topics/:id` endpoint (requires Trainer with specialization assignment) soft-deleting topic
9. Backend enforces access control: users can only create/edit modules and topics in their assigned specializations
10. Local testability: Trainer user creates module "Backend Fundamentals" with topic "RESTful APIs" and retrieves it via GET endpoint

### Story 2.3: Rich Text Content Editor for Topic Creation

**As a** Trainer or TA,
**I want** a rich text editor to create and format topic content,
**so that** I can include headings, lists, code blocks, and emphasis in training materials.

**Acceptance Criteria:**

1. Frontend implements Topic Editor page (route: `/modules/:moduleId/topics/:topicId/edit`) with rich text editor component using Quill or TipTap library
2. Editor toolbar includes formatting options: bold, italic, underline, headings (H1-H3), bullet lists, numbered lists, code block, blockquote, links
3. Editor supports pasting formatted text from Word/Google Docs with reasonable formatting preservation
4. Editor auto-saves draft to browser localStorage every 30 seconds to prevent data loss
5. "Save" button calls `PATCH /api/topics/:id` endpoint with HTML content; displays success toast notification on save
6. "Preview" toggle switches between edit mode and rendered HTML view showing how content will appear to trainees
7. Editor enforces access control: only Trainers and TAs assigned to topic's specialization can access editor; others see 403 error page
8. Frontend implements "Create New Topic" flow: Trainer clicks "Add Topic" button on module page → modal prompts for topic name → redirects to Topic Editor for new topic
9. Local testability: Trainer creates topic with formatted content including headings, code blocks, and lists; saves successfully; preview renders correctly

### Story 2.4: Content Asset Upload and Storage

**As a** Trainer,
**I want** to upload images, PDFs, videos, and code files as topic assets,
**so that** I can enrich training content with supplementary materials.

**Acceptance Criteria:**

1. Database migration creates `content_assets` table with columns: id (UUID), topic_id (FK to topics), file_name (text), file_type (enum: image, pdf, video, code, other), file_size_bytes (integer), storage_url (text, Azure Blob URL), uploaded_by_user_id (FK to users), created_at
2. Backend implements Azure Blob Storage integration using `@azure/storage-blob` SDK with container `tcms-content-assets`
3. Backend exposes `POST /api/topics/:topicId/assets` endpoint (requires Trainer/TA with specialization access) accepting multipart file upload (max 50MB)
4. Endpoint validates file type against allowed types: images (jpg, png, gif, svg), PDFs, videos (mp4, webm), code files (txt, js, py, java, etc.), zip archives
5. Endpoint uploads file to Azure Blob Storage with naming convention: `topics/{topicId}/{uuid}-{filename}`
6. Endpoint inserts metadata into `content_assets` table and returns asset object with storage_url (signed URL with 1-hour expiry for immediate access)
7. Backend exposes `GET /api/topics/:topicId/assets` endpoint returning list of all assets for a topic
8. Backend exposes `DELETE /api/assets/:id` endpoint (requires Trainer with specialization access) deleting asset from both database and blob storage
9. Frontend adds "Upload Asset" button to Topic Editor opening file picker dialog
10. Frontend displays uploaded assets below editor as list with file name, type icon, size, and delete button
11. Frontend allows inserting asset links into rich text content (e.g., image embed, PDF download link)
12. Local testability: Trainer uploads an image and PDF to topic, inserts image into content body, saves topic, and verifies asset accessible via storage_url

### Story 2.5: Content Version History and Rollback

**As a** Trainer,
**I want** to view version history of topic content changes and rollback to previous versions if needed,
**so that** I can recover from accidental deletions or unwanted edits.

**Acceptance Criteria:**

1. Database migration creates `topic_versions` table with columns: id (UUID), topic_id (FK to topics), content (text, snapshot of HTML), version_number (integer), changed_by_user_id (FK to users), change_description (text, nullable), created_at
2. Backend automatically creates version record in `topic_versions` table whenever `PATCH /api/topics/:id` is called with content change
3. Version_number auto-increments per topic (e.g., topic's first edit is v1, second edit is v2)
4. Backend exposes `GET /api/topics/:id/versions` endpoint returning list of versions with metadata: version_number, changed_by user name, created_at (no content in list for performance)
5. Backend exposes `GET /api/topics/:id/versions/:versionNumber` endpoint returning full content HTML for specific version
6. Backend exposes `POST /api/topics/:id/rollback` endpoint (requires Trainer role with specialization access) accepting version_number; restores topic content to that version and creates new version record documenting rollback action
7. Frontend implements "Version History" button on Topic Editor opening modal/sidebar showing version list
8. Frontend displays version list as timeline with version number, author, timestamp, and "View" and "Restore" actions
9. "View" action displays version content in read-only preview modal
10. "Restore" action prompts confirmation ("Are you sure you want to restore to version X?"), then calls rollback endpoint and refreshes editor
11. Local testability: Trainer edits topic content twice, views version history showing v1 and v2, restores to v1, and verifies content reverted

### Story 2.6: Bulk Content Import from Microsoft Loop

**As a** Head of Training Center,
**I want** to bulk import existing training content from Microsoft Loop,
**so that** we can migrate historical materials into TCMS without manual re-entry.

**Acceptance Criteria:**

1. Backend implements CLI script `npm run import:content` accepting path to directory containing exported Loop content (HTML files or markdown files organized by module/topic)
2. Script expects folder structure: `{Specialization}/{Module}/{Topic}.md` or `.html`
3. Script parses folder structure and creates corresponding specializations (if not exists), modules, and topics in database
4. Script reads file content and converts markdown to HTML (using library like `marked`) or preserves HTML if already formatted
5. Script assigns content authorship to a designated "System Importer" user or prompts for user_id
6. Script validates imported content doesn't duplicate existing modules/topics (checks by name)
7. Script provides progress output: "Importing Backend → Python Basics → Variables (Topic 1/45)..."
8. Script generates summary report at completion: X specializations, Y modules, Z topics imported; lists any errors/skipped files
9. Script is idempotent: re-running with same data does not create duplicates (checks before insert)
10. Documentation added to README explaining export process from Microsoft Loop (if documented) and how to run import script
11. Local testability: Developer creates test content folder structure with sample markdown files, runs import script, verifies modules and topics appear in database and are viewable in UI

### Story 2.7: Content Organization UI for Trainees

**As a** Trainee,
**I want** to browse the curriculum structure and view topic content,
**so that** I can learn the training materials in my specialization.

**Acceptance Criteria:**

1. Frontend implements Learning Dashboard (route: `/learn`) showing trainee's assigned specialization with list of modules as expandable cards
2. Each module card displays: module name, description, topic count, completion status (X/Y topics completed)
3. Clicking module card expands inline or navigates to Module Detail page showing list of topics with: topic name, status icon (not started, in progress, completed), action button "View Content" or "Continue"
4. Frontend implements Topic Content View (route: `/learn/topics/:topicId`) displaying topic HTML content rendered from database with embedded assets (images, code blocks)
5. Topic view includes navigation sidebar showing current module's topic list for easy jumping between topics
6. Topic view includes progress indicator at top showing "Topic X of Y" within module
7. Topic view includes "Mark as Complete" button (visible only if topic's assessments passed—deferred to Epic 5 for now, button can be placeholder)
8. Frontend displays breadcrumb navigation: Specialization > Module > Topic for context
9. Content is responsive and readable on tablet (768px+) and desktop viewports
10. Local testability: Trainee user logs in, navigates to Learning Dashboard, selects a module, views topic content, and sees rendered HTML with correct formatting

---

## Epic 3: Self-Paced Learning & Progress Tracking

**Goal:** Enable trainees to track their learning progress at the topic and module levels, view deadlines, and access a personalized dashboard showing completion status, upcoming deadlines, and recommended next actions. This epic establishes the trainee experience foundation and provides visibility into self-paced learning with deadline accountability.

### Story 3.1: Trainee Progress Data Model and Tracking

**As a** trainee,
**I want** my progress through topics and modules automatically tracked,
**so that** I can see what I have completed and what remains.

**Acceptance Criteria:**

1. Database migration creates `trainee_progress` table with columns: id (UUID), trainee_id (FK to users), topic_id (FK to topics), status (enum: not_started, in_progress, completed), started_at (timestamp, nullable), completed_at (timestamp, nullable), updated_at
2. Database creates unique constraint on (trainee_id, topic_id) to ensure one progress record per trainee per topic
3. Backend exposes `GET /api/trainees/me/progress` endpoint returning trainee's progress for all topics in their assigned specialization with module grouping
4. Backend exposes `PATCH /api/trainees/progress/:topicId` endpoint updating topic progress status (in_progress or completed) with timestamps; trainee can only update their own progress
5. Backend implements automatic progress initialization: when trainee first views a topic (GET `/api/topics/:id` called), create progress record with status `in_progress` if not exists
6. Backend calculates module completion as: all topics within module have status `completed`
7. Backend exposes `GET /api/trainees/me/stats` endpoint returning: total topics in specialization, topics completed, topics in progress, modules completed, overall completion percentage
8. Unit tests created for progress tracking logic covering: initial progress creation, status updates, completion calculation
9. Local testability: Trainee views topic, verifies progress record created with status `in_progress`; manually updates to `completed` via API, verifies timestamp set

### Story 3.2: Module Deadlines Configuration

**As a** Head of Training Center,
**I want** to set module deadlines per cohort,
**so that** trainees have clear time expectations for completing each module.

**Acceptance Criteria:**

1. Database migration creates `cohort_module_deadlines` table with columns: id (UUID), cohort_id (FK to cohorts), module_id (FK to modules), deadline_date (date), created_at, updated_at
2. Database creates unique constraint on (cohort_id, module_id) to ensure one deadline per module per cohort
3. Backend exposes `POST /api/admin/cohorts/:cohortId/deadlines` endpoint (requires HeadOfProgram or HeadOfTrainingCenter role) accepting module_id and deadline_date
4. Backend exposes `GET /api/cohorts/:cohortId/deadlines` endpoint returning all module deadlines for a cohort
5. Backend exposes `PATCH /api/admin/cohorts/:cohortId/deadlines/:moduleId` endpoint updating deadline_date for a module
6. Backend exposes `DELETE /api/admin/cohorts/:cohortId/deadlines/:moduleId` endpoint removing deadline
7. Frontend implements Cohort Deadlines management page (route: `/admin/cohorts/:cohortId/deadlines`) accessible to Heads showing table of modules with assigned deadlines
8. Frontend allows bulk deadline setting: select multiple modules, choose date via date picker, apply to all selected modules
9. Frontend displays warning if deadline_date is in the past or less than 7 days from current date
10. Local testability: Admin sets deadline for "Backend Fundamentals" module in "GTP 2026 Q1" cohort to 30 days from today; verifies deadline appears in cohort deadlines list

### Story 3.3: On-Time vs Late Completion Tracking

**As a** Head of Program,
**I want** to track whether trainees completed modules before or after deadlines,
**so that** I can identify at-risk trainees and assess accountability.

**Acceptance Criteria:**

1. Database migration adds `on_time` column (boolean) to `trainee_progress` table for module-level tracking
2. Backend implements business logic: when trainee completes all topics in a module (achieving module completion), determine if current date <= deadline_date from `cohort_module_deadlines`; set `on_time = true` if before/on deadline, `on_time = false` if after deadline
3. If no deadline set for module, `on_time` remains null (not applicable)
4. Backend exposes `GET /api/trainees/me/progress/modules` endpoint returning module-level progress for trainee with fields: module_id, module_name, topics_completed, topics_total, deadline_date, completion_date, on_time status
5. Backend exposes `GET /api/admin/cohorts/:cohortId/trainees/progress` endpoint (requires Head roles) returning all trainees' module completion status with on_time flags for cohort analytics
6. Frontend displays on-time status on trainee dashboard: green checkmark icon for on-time completion, red warning icon for late completion, yellow clock icon for approaching deadline (within 3 days)
7. Frontend displays deadline urgency on Learning Dashboard: modules sorted by deadline proximity (soonest first)
8. Local testability: Trainee completes module before deadline, verifies on_time = true; advance system date past deadline, complete another module, verify on_time = false

### Story 3.4: Trainee Dashboard - Progress Visualization

**As a** trainee,
**I want** a dashboard showing my overall progress, recent scores, and upcoming deadlines,
**so that** I can quickly assess where I stand and what to focus on next.

**Acceptance Criteria:**

1. Frontend implements Trainee Dashboard (route: `/dashboard`) as default landing page for trainee role after login
2. Dashboard displays header card with trainee name, assigned specialization, and cohort name
3. Dashboard displays "Progress Overview" section with circular progress ring showing overall completion percentage (topics completed / total topics) with animated fill effect
4. Dashboard displays "Module Progress" section with horizontal cards for each module showing: module name, completion bar (topics completed / total), deadline date, on-time status icon
5. Dashboard displays "Upcoming Deadlines" section with timeline list of next 5 deadlines sorted by urgency with countdown (e.g., "3 days remaining")
6. Dashboard displays "Recent Activity" section showing last 5 topics viewed or completed with timestamps
7. Dashboard displays "Recommended Next Steps" card suggesting next action based on progress (e.g., "Complete Module 2 Lab by Oct 30" or "Continue Topic: Variables and Data Types")
8. Dashboard content is loaded via API call to `/api/trainees/me/dashboard` returning aggregated data (progress, deadlines, recent activity, recommendations)
9. Dashboard is responsive and displays correctly on tablet and desktop viewports
10. Local testability: Trainee logs in, views dashboard showing progress ring at 30%, 2 upcoming deadlines within 7 days, and recommended action to complete next topic

### Story 3.5: Module Completion Status and Achievement

**As a** trainee,
**I want** to see clear visual indicators when I complete modules,
**so that** I have a sense of accomplishment and clarity on my progress.

**Acceptance Criteria:**

1. Backend updates `trainee_progress` to include module-level completion record: when all topics in module are completed, create aggregate record marking module as completed with completion_date
2. Frontend displays completion badge on module cards when module is 100% complete (all topics completed)
3. Frontend displays celebratory modal/toast notification when trainee completes the last topic in a module: "Congratulations! You completed [Module Name]!"
4. Frontend adds completed modules to "Completed Modules" section on trainee dashboard with completion dates
5. Frontend grays out or collapses completed modules in Learning view to reduce visual clutter and emphasize remaining work
6. Frontend includes "Show Completed Modules" toggle on Learning Dashboard to expand/collapse completed items
7. Local testability: Trainee completes all topics in a module, sees completion modal, verifies module marked as completed on dashboard and Learning view

### Story 3.6: Deadline Notifications and Reminders

**As a** trainee,
**I want** to receive email notifications for upcoming and missed deadlines,
**so that** I stay accountable and don't miss important milestones.

**Acceptance Criteria:**

1. Backend implements scheduled job (using Bull queue) running daily at 8am WAT checking for upcoming deadlines
2. Job queries `cohort_module_deadlines` joined with trainee enrollments, identifying trainees with incomplete modules where deadline is in 3 days
3. Job sends email to each trainee with subject "Reminder: [Module Name] deadline in 3 days" with email body including: module name, deadline date, current completion status, link to module in TCMS
4. Job repeats notification at 1 day before deadline with subject "Urgent: [Module Name] deadline tomorrow"
5. Job identifies trainees who missed deadlines (current date > deadline_date and module incomplete) and sends "Missed Deadline: [Module Name]" email daily until module completed
6. Email templates created using HTML with TCMS branding and clear call-to-action buttons
7. Backend exposes `GET /api/trainees/me/notifications/preferences` endpoint returning notification settings (email enabled/disabled per notification type)
8. Backend exposes `PATCH /api/trainees/me/notifications/preferences` endpoint allowing trainees to toggle email notifications (default: all enabled)
9. Backend respects notification preferences: only send emails if trainee has enabled that notification type
10. Local testability: Developer triggers notification job manually via CLI command, verifies emails sent to test trainees; trainee disables deadline reminders, verifies no email sent on next job run

---

## Epic 4: AI-Powered Assessment Generation & Management

**Goal:** Implement AI-powered question generation for Knowledge Checks (KCs) and Module Assessments (MAs) using OpenAI GPT-4 or Anthropic Claude, with trainer review workflows for quality control. This epic enables trainers to generate, review, edit, approve, and manage question pools, dramatically reducing assessment creation time while maintaining quality standards.

### Story 4.1: AI Question Generation Data Model

**As a** developer,
**I want** a data model for storing AI-generated questions with metadata,
**so that** questions can be managed, reviewed, and presented to trainees.

**Acceptance Criteria:**

1. Database migration creates `assessment_types` table with columns: id (UUID), name (enum: KnowledgeCheck, ModuleAssessment), abbreviation (KC, MA), created_at
2. Database seeds `assessment_types` with KC and MA records
3. Database migration creates `questions` table with columns: id (UUID), topic_id (FK to topics), assessment_type_id (FK to assessment_types), question_text (text), question_type (enum: single_choice, multiple_choice, coding_analysis), options (JSONB array of {label, text, is_correct}), difficulty (enum: moderate, hard, very_hard), generated_by_ai (boolean), reviewed_by_user_id (FK to users, nullable), approved (boolean, default false), approval_date (timestamp, nullable), created_at, updated_at
4. Database creates index on (topic_id, assessment_type_id, approved) for efficient querying of approved question pools
5. Database migration creates `question_performance` table with columns: id (UUID), question_id (FK to questions), attempts_count (integer), correct_count (integer), success_rate (float, calculated), flagged_for_review (boolean), updated_at
6. Local testability: Developer inserts test question record manually via SQL and retrieves via `SELECT * FROM questions WHERE topic_id = ?`

### Story 4.2: AI Question Generation Service Integration

**As a** Trainer,
**I want** to trigger AI generation of questions for a topic,
**so that** I can quickly create assessment content without manual writing.

**Acceptance Criteria:**

1. Backend implements AI integration service using OpenAI GPT-4 API (or Anthropic Claude) with configurable API key from environment variable
2. Backend exposes `POST /api/topics/:topicId/generate-questions` endpoint (requires Trainer role with specialization access) accepting parameters: assessment_type (KC or MA), question_count (default 30)
3. Endpoint retrieves topic content from database and constructs prompt for AI:
   - "Generate {question_count} {difficulty} multiple-choice questions based on the following content. Each question should test practical understanding. Include 4 options per question with only one correct answer. Output as JSON array: [{question_text, options: [{label: 'A', text, is_correct}], difficulty}]"
   - Difficulty = "moderate to hard" for KC, "very hard" for MA
4. Backend sends prompt to AI API, parses JSON response, validates structure (question_text and 4 options with exactly one is_correct=true)
5. Backend inserts each question into `questions` table with generated_by_ai=true, approved=false
6. Backend enqueues question generation as background job (using Bull) to avoid blocking HTTP request; returns job_id to frontend
7. Backend exposes `GET /api/jobs/:jobId/status` endpoint returning job status (pending, completed, failed) and result (generated question IDs) once complete
8. Frontend implements "Generate Questions" button on Topic Editor page opening modal to select assessment type and question count
9. Frontend displays loading indicator while job processes; polls job status endpoint every 2 seconds until completion
10. Frontend displays success message "Generated 30 questions for review" with link to question review page
11. Frontend displays error message if AI generation fails (API error, rate limit, invalid content) with retry option
12. Unit tests mock AI API calls and verify prompt construction and response parsing
13. Local testability: Trainer triggers question generation for test topic, waits for job completion, verifies 30 questions inserted in database with approved=false

### Story 4.3: Selectable Assessment Generation Criteria

**As a** Trainer,
**I want** to customize the AI question generation by selecting specific criteria like difficulty, cognitive level, and question types,
**so that** I can generate assessments tailored to my learning objectives and trainee skill levels.

**Acceptance Criteria:**

1. Database migration adds `generation_criteria` column (JSONB) to `questions` table storing the criteria used for generation: {difficulty, question_types, question_count, cognitive_levels, focus_areas, question_distribution, scenario_preference}
2. Database migration creates `generation_presets` table with columns: id (UUID), trainer_id (FK to users), preset_name (text), criteria (JSONB, same structure as questions.generation_criteria), specialization_id (FK to specializations, nullable), is_default (boolean), created_at, updated_at
3. Backend updates `POST /api/topics/:topicId/generate-questions` endpoint to accept additional optional parameters:
   - difficulty_level (enum: easy, moderate, hard, very_hard, mixed; defaults based on assessment_type)
   - question_types (array: ['single_choice', 'multiple_choice', 'coding_analysis']; default all types)
   - question_count (integer: 10-50; default 30)
   - cognitive_levels (array: ['remember', 'understand', 'apply', 'analyze', 'evaluate', 'create']; default all levels)
   - focus_areas (text array: optional keywords/subtopics to emphasize)
   - question_distribution (enum: even, weighted, challenging_only; default even)
   - include_scenarios (boolean: whether to include real-world scenarios; default true)
   - include_code_debugging (boolean: whether to include code debugging questions; default true for technical specializations)
   - include_best_practices (boolean: whether to include best practices questions; default true)
4. Backend constructs enhanced AI prompt incorporating selected criteria:
   - Base prompt structure: "Generate {question_count} multiple-choice questions with {difficulty_level} difficulty focusing on {cognitive_levels} cognitive skills based on Bloom's Taxonomy."
   - If focus_areas provided: "Emphasize the following topics: {focus_areas}."
   - If question_distribution is weighted: "Distribute questions with 50% on core concepts, 30% on advanced topics, 20% on edge cases."
   - If question_distribution is challenging_only: "Focus exclusively on challenging concepts that typically cause confusion."
   - If include_scenarios=true: "Include real-world scenario-based questions where applicable."
   - If include_code_debugging=true: "Include questions that require analyzing and debugging code snippets."
   - If include_best_practices=true: "Include questions about industry best practices and standards."
   - Question type distribution based on question_types array
5. Backend stores complete generation_criteria as JSONB in questions table for each generated question for audit and analysis purposes
6. Backend exposes `POST /api/generation-presets` endpoint (requires Trainer role) creating reusable preset with: preset_name, criteria (JSONB), specialization_id (optional), is_default (boolean)
7. Backend exposes `GET /api/generation-presets` endpoint (requires Trainer role) returning trainer's saved presets filtered by specialization_id if provided
8. Backend exposes `GET /api/generation-presets/:id` endpoint returning specific preset details
9. Backend exposes `DELETE /api/generation-presets/:id` endpoint allowing trainers to delete their own presets
10. Frontend enhances "Generate Questions" modal with tabbed interface:
    - **Tab 1: Basic Settings** - Assessment type (KC/MA), Question count (slider 10-50), Quick presets (dropdown showing saved presets or "Custom")
    - **Tab 2: Difficulty & Types** - Difficulty level (radio buttons: Easy/Moderate/Hard/Very Hard/Mixed), Question types (checkboxes: Single Choice/Multiple Choice/Coding Analysis)
    - **Tab 3: Cognitive Level** - Bloom's Taxonomy checkboxes (Remember/Understand/Apply/Analyze/Evaluate/Create) with visual pyramid diagram
    - **Tab 4: Focus & Distribution** - Focus areas (textarea for comma-separated keywords), Question distribution (radio: Even/Weighted/Challenging Only)
    - **Tab 5: Advanced Options** - Include scenarios (toggle), Include code debugging (toggle), Include best practices (toggle)
11. Frontend displays "Save as Preset" button in modal allowing trainers to save current criteria configuration with a name
12. Frontend displays "Load Preset" dropdown populated with trainer's saved presets; selecting preset auto-fills all criteria fields
13. Frontend displays preset indicator on Topic Editor showing which preset was used for last generation (e.g., "Last generated using: Backend Fundamentals - Standard KC")
14. Frontend validates criteria combinations: warn if conflicting selections (e.g., "Easy" difficulty with "Create" cognitive level)
15. Frontend displays criteria summary before generation: "You are about to generate 40 Hard questions focusing on Apply and Analyze cognitive levels with real-world scenarios."
16. Frontend shows generated questions metadata in Question Review page: displays generation criteria used (difficulty, cognitive level, etc.) for transparency
17. Unit tests verify prompt construction with various criteria combinations and JSONB storage/retrieval
18. Local testability: Trainer opens generate modal, selects "Hard" difficulty, "Apply + Analyze" cognitive levels, 40 questions, saves as preset "Backend Advanced", generates questions, verifies criteria stored in database and questions reflect selected parameters

### Story 4.4: Question Review Interface for Trainers

**As a** Trainer,
**I want** to review AI-generated questions before they are used in assessments,
**so that** I can ensure quality, accuracy, and appropriate difficulty.

**Acceptance Criteria:**

1. Backend exposes `GET /api/topics/:topicId/questions/pending-review` endpoint (requires Trainer role) returning all unapproved questions for a topic filtered by assessment_type with pagination
2. Backend exposes `PATCH /api/questions/:id` endpoint (requires Trainer role) allowing updates to question_text, options, difficulty, and question_type
3. Backend exposes `POST /api/questions/:id/approve` endpoint (requires Trainer role) setting approved=true, approval_date=now, reviewed_by_user_id=current_user
4. Backend exposes `POST /api/questions/:id/reject` endpoint (requires Trainer role) deleting question from database
5. Backend exposes `POST /api/questions/:id/regenerate` endpoint (requires Trainer role) marking question for regeneration, enqueuing background job to call AI API again for replacement question
6. Frontend implements Question Review page (route: `/topics/:topicId/questions/review`) showing list of pending questions with cards displaying: question_text, options (with correct answer highlighted), difficulty, and action buttons (Edit, Approve, Reject, Regenerate)
7. Frontend implements inline editing: clicking "Edit" opens modal with form fields pre-populated; saves changes via PATCH endpoint
8. Frontend implements bulk actions: checkboxes on question cards allow selecting multiple questions for bulk approval or rejection
9. Frontend displays question counter: "Pending Review: X questions" and "Approved: Y questions"
10. Frontend allows filtering questions by assessment_type (KC, MA) and difficulty
11. Local testability: Trainer views pending questions, edits one question's text, approves it, verifies approved=true in database; rejects another question, verifies deleted from database

### Story 4.5: Hybrid Workflow - Auto-Publish KC, Review MA

**As a** Trainer,
**I want** Knowledge Checks to auto-publish after generation but Module Assessments to require my review,
**so that** I balance efficiency with quality control for high-stakes assessments.

**Acceptance Criteria:**

1. Backend implements configuration parameter `AUTO_APPROVE_KC` (default true) and `AUTO_APPROVE_MA` (default false) in environment variables
2. During AI question generation (Story 4.2), after inserting questions into database:
   - If assessment_type = KC and AUTO_APPROVE_KC = true, automatically set approved=true for all generated KC questions
   - If assessment_type = MA, leave approved=false (requires manual review regardless of setting)
3. Backend exposes `GET /api/settings/question-approval-policy` endpoint (requires Trainer or Head roles) returning current policy: KC_mode (auto/review), MA_mode (auto/review)
4. Backend exposes `PATCH /api/admin/settings/question-approval-policy` endpoint (requires HeadOfTrainingCenter role) allowing toggling AUTO_APPROVE_KC setting
5. Frontend displays configuration banner on Question Review page: "Knowledge Checks: Auto-Published | Module Assessments: Review Required"
6. Frontend displays different UI flows:
   - After KC generation: "30 Knowledge Check questions generated and published" (no review page redirect)
   - After MA generation: "30 Module Assessment questions generated. Review required before use" (redirect to review page)
7. Frontend shows toggle switch on Settings page (accessible to HeadOfTrainingCenter) to enable/disable auto-publish for KCs with warning: "Disabling auto-publish requires trainer review for all questions"
8. Local testability: Trainer generates KC questions with auto-approve enabled, verifies all marked approved=true immediately; generates MA questions, verifies approved=false and requires manual review

### Story 4.6: Question Pool Management and Selection

**As a** system,
**I want** to maintain pools of approved questions and randomly select subsets for each trainee's assessment attempt,
**so that** assessments are unique and prevent memorization or cheating.

**Acceptance Criteria:**

1. Backend implements question pool logic: when trainee starts assessment (Story 5.1 in next epic), query approved questions for topic and assessment_type, randomly select N questions (configurable, default 20 for KC, 15 for MA)
2. Backend ensures selected questions are a subset of total pool (if pool has 30 questions, select random 20; if pool has 50 questions, select random 20)
3. Backend exposes `GET /api/topics/:topicId/question-pool-stats` endpoint (requires Trainer role) returning: total_questions, approved_questions, pending_questions, questions_per_attempt (from configuration)
4. Backend warns trainers if approved question pool is insufficient: if approved_questions < questions_per_attempt, return warning flag in endpoint response
5. Frontend displays question pool stats on Topic Editor page: "Question Pool: 35 approved KC questions (20 per attempt), 28 approved MA questions (15 per attempt)"
6. Frontend displays warning banner if pool insufficient: "Warning: Only 12 approved KC questions available. Minimum 20 required. Generate or approve more questions."
7. Backend configuration allows Head of Training Center to set questions_per_attempt via `PATCH /api/admin/settings/assessment-config` endpoint
8. Local testability: Developer verifies random selection logic by triggering multiple assessment attempts and confirming different question subsets selected each time (tested in Story 5.1)

### Story 4.7: Question Performance Analytics and Flagging

**As a** Trainer,
**I want** to see how trainees perform on each question and flag poorly performing questions,
**so that** I can identify flawed questions and improve assessment quality.

**Acceptance Criteria:**

1. Backend updates `question_performance` record after each trainee's assessment attempt (logic implemented in Epic 5, data model prepared here)
2. Backend calculates success_rate = (correct_count / attempts_count) for each question
3. Backend flags questions for review if success_rate < 0.30 (too hard/confusing) or success_rate > 0.90 (too easy) after minimum 10 attempts
4. Backend exposes `GET /api/topics/:topicId/questions/analytics` endpoint (requires Trainer or Head role) returning all approved questions with performance metrics: question_id, question_text, attempts_count, success_rate, flagged_for_review
5. Frontend implements Question Analytics page (route: `/topics/:topicId/questions/analytics`) displaying table of questions sorted by success_rate with color coding: red for <30%, green for 30-90%, yellow for >90%
6. Frontend highlights flagged questions with warning icon and "Flagged for Review" badge
7. Frontend allows trainer to click flagged question to view details, edit, or replace
8. Frontend displays aggregate analytics: average success rate across all questions, distribution chart showing difficulty balance
9. Local testability: Developer seeds question_performance data with various success rates, verifies flagging logic correctly identifies questions <30% or >90%, views analytics page showing flagged questions

### Story 4.8: Manual Question Creation as Fallback

**As a** Trainer,
**I want** to manually create questions without using AI generation,
**so that** I can supplement AI-generated content or create questions for topics where AI struggles.

**Acceptance Criteria:**

1. Backend exposes `POST /api/topics/:topicId/questions` endpoint (requires Trainer role with specialization access) accepting: assessment_type, question_text, question_type, options (array), difficulty
2. Endpoint validates options array: single_choice requires exactly 1 is_correct=true option and 4 total options; multiple_choice requires 1+ is_correct=true options
3. Endpoint inserts question into `questions` table with generated_by_ai=false, approved=true (manual questions auto-approved)
4. Frontend implements "Create Question Manually" button on Topic Editor opening modal with form fields: assessment type (dropdown), question type (dropdown), question text (textarea), options (dynamic form allowing 2-6 options with correct answer checkboxes), difficulty (dropdown)
5. Frontend validates form: ensures at least one correct answer selected, all options filled, question text non-empty
6. Frontend displays success message "Question created and added to pool" after submission
7. Frontend allows editing manually created questions via same Question Review interface (Story 4.4)
8. Local testability: Trainer manually creates a KC question with 4 options, submits, verifies question appears in approved pool and is selectable for assessments

---

## Epic 5: Assessment Taking & Auto-Grading

**Goal:** Enable trainees to take randomized assessments (Knowledge Checks and Module Assessments) with attempt limits, auto-grading for MCQ questions, immediate feedback, and answer reveals after attempts exhausted. This epic completes the assessment workflow, allowing trainees to demonstrate knowledge and receive instant results.

### Story 5.1: Assessment Attempt Data Model and Initialization

**As a** trainee,
**I want** to start an assessment attempt for a topic,
**so that** I can test my knowledge.

**Acceptance Criteria:**

1. Database migration creates `assessment_attempts` table with columns: id (UUID), trainee_id (FK to users), topic_id (FK to topics), assessment_type_id (FK to assessment_types), attempt_number (integer), started_at (timestamp), submitted_at (timestamp, nullable), score (float, nullable), passed (boolean, nullable), questions_snapshot (JSONB array of selected question IDs and trainee answers), created_at
2. Database creates index on (trainee_id, topic_id, assessment_type_id) for querying attempt history
3. Backend exposes `POST /api/topics/:topicId/assessments/:assessmentType/start` endpoint (requires Trainee role) initializing new assessment attempt
4. Endpoint validates attempt limits:
   - Query existing attempts for trainee, topic, and assessment_type
   - If assessment_type = KC and attempts >= 3, return 400 error "Maximum attempts reached"
   - If assessment_type = MA and attempts >= 2, return 400 error "Maximum attempts reached"
   - If trainee already passed assessment (passed=true in any attempt), return 400 error "You have already passed this assessment. Retaking is not allowed."
5. Endpoint randomly selects questions from approved question pool (20 for KC, 15 for MA as per Story 4.5)
6. Endpoint inserts `assessment_attempts` record with attempt_number (incremented from previous attempts), selected question IDs in questions_snapshot, started_at=now
7. Endpoint returns attempt object with: attempt_id, questions array (id, question_text, options - without is_correct), time_limit (nullable for MVP, future enhancement)
8. Unit tests verify attempt limit enforcement and passed-check logic
9. Local testability: Trainee starts KC attempt for topic, verifies attempt_number=1, questions array contains 20 randomized questions; starts second attempt, verifies attempt_number=2

### Story 5.2: Assessment Taking Interface

**As a** trainee,
**I want** a clean interface to read questions and select answers,
**so that** I can focus on demonstrating my knowledge without distractions.

**Acceptance Criteria:**

1. Frontend implements Assessment Taking page (route: `/assessments/:attemptId`) displaying one question at a time (single-page view) or all questions in scrollable list (multi-page view configurable in settings)
2. For single-page view: Display question number (e.g., "Question 5 of 20"), question text, options as radio buttons (single_choice) or checkboxes (multiple_choice), "Previous" and "Next" navigation buttons
3. For multi-page view: Display all questions in vertical list with numbered headers, options as radio/checkboxes, "Submit Assessment" button at bottom
4. Frontend stores trainee's selected answers in component state (not persisted to backend until submission for performance)
5. Frontend displays progress indicator: "Answered: 12/20 questions" and highlights unanswered questions in navigation
6. Frontend includes "Review Answers" step before submission showing summary: question number, selected answer(s), with "Change Answer" links
7. Frontend prompts confirmation modal on submit: "Are you sure you want to submit? You cannot change answers after submission."
8. Frontend displays timer (if time_limit set in future, placeholder UI for MVP)
9. Frontend is responsive and functional on tablet and desktop viewports
10. Local testability: Trainee starts assessment, selects answers for all questions, reviews answers, submits assessment, verifies answers sent to backend

### Story 5.3: Assessment Submission and Auto-Grading

**As a** trainee,
**I want** my assessment auto-graded immediately after submission,
**so that** I receive instant feedback on my performance.

**Acceptance Criteria:**

1. Backend exposes `POST /api/assessments/:attemptId/submit` endpoint (requires Trainee role, validates trainee owns attempt) accepting answers payload: array of {question_id, selected_option_labels (e.g., ['A'] or ['B', 'C'])}
2. Endpoint validates all questions answered (or allow partial submission based on requirements—assume required for now)
3. Endpoint retrieves correct answers from `questions` table for each question_id in attempt
4. Endpoint calculates score:
   - For each question: if selected_option_labels match all is_correct=true options (exact match for both single and multiple choice), mark correct; else incorrect
   - Score = (correct_count / total_questions) * 100
5. Endpoint determines passed status:
   - KC passing threshold: 70% (configurable via `KC_PASSING_THRESHOLD` environment variable)
   - MA passing threshold: 75% (configurable via `MA_PASSING_THRESHOLD` environment variable)
   - If score >= threshold, passed=true; else passed=false
6. Endpoint updates `assessment_attempts` record: submitted_at=now, score, passed, questions_snapshot includes trainee's selected answers
7. Endpoint updates `question_performance` table: increment attempts_count and correct_count (if answered correctly) for each question
8. If trainee passed assessment and this is first pass for this topic+assessment_type, update `trainee_progress` accordingly (topic marked in_progress or completed based on both KC and MA status)
9. Endpoint returns result object: score, passed, total_questions, correct_count, incorrect_count, attempt_number, attempts_remaining
10. Unit tests cover grading logic for single-choice and multiple-choice questions, passing threshold calculation
11. Local testability: Trainee submits assessment with known answers, verifies score calculated correctly, passed status accurate; submits with all wrong answers, verifies failed status

### Story 5.4: Assessment Results Display

**As a** trainee,
**I want** to see my score and which questions I answered correctly or incorrectly,
**so that** I can learn from my mistakes.

**Acceptance Criteria:**

1. Frontend implements Assessment Results page (route: `/assessments/:attemptId/results`) displaying:
   - Header: "Assessment Results" with pass/fail badge (green "Passed" or red "Failed")
   - Score summary: "You scored 85% (17/20 correct)"
   - Attempts summary: "Attempt 2 of 3" with visual indicator (2 filled circles, 1 empty)
   - Message: If passed: "Congratulations! You passed this assessment." If failed and attempts remain: "You can retry this assessment. X attempts remaining." If failed and no attempts: "You have used all attempts. See correct answers below."
2. Frontend displays question-by-question breakdown:
   - For each question: question number, question text, trainee's selected answer(s) highlighted, correctness indicator (green checkmark if correct, red X if incorrect)
   - If attempts exhausted OR assessment passed, display correct answer(s) highlighted in green
   - If attempts remaining and not passed, hide correct answers (show only trainee's correctness)
3. Frontend includes "Retry Assessment" button (visible only if attempts remaining and not passed) redirecting to new attempt
4. Frontend includes "Return to Learning Dashboard" button
5. Frontend allows trainee to review past attempts: Assessment History link showing all attempts with scores and dates
6. Local testability: Trainee views results after passing, sees correct answers revealed; views results after failing with attempts left, correct answers hidden; views results after exhausting attempts, correct answers revealed

### Story 5.5: Topic Completion Based on Assessment Passage

**As a** trainee,
**I want** my topic marked completed only after passing both KC and MA,
**so that** my progress accurately reflects mastery of the material.

**Acceptance Criteria:**

1. Backend implements topic completion logic: when trainee passes assessment (passed=true in assessment_attempts), check if both KC and MA are passed for the topic
2. Query `assessment_attempts` for trainee and topic: find latest passed attempt for KC, find latest passed attempt for MA
3. If both KC and MA have passed=true attempts, update `trainee_progress` for the topic: status=completed, completed_at=now
4. If only one assessment passed, update `trainee_progress` to status=in_progress (partial completion)
5. Backend exposes `GET /api/topics/:topicId/completion-status` endpoint (requires Trainee role) returning: kc_passed (boolean), ma_passed (boolean), topic_completed (boolean)
6. Frontend displays completion status on Topic Content View page: "Progress: KC Passed ✓ | MA Not Attempted" or "Progress: KC Passed ✓ | MA Passed ✓ | Topic Completed 🎉"
7. Frontend updates trainee dashboard progress ring and module completion status in real-time after assessment completion
8. Frontend displays celebratory modal when topic completed: "You completed [Topic Name]! Keep up the great work."
9. Local testability: Trainee passes KC, verifies topic status=in_progress; passes MA, verifies topic status=completed and completion_at timestamp set; dashboard reflects updated progress

### Story 5.6: Assessment Attempt History and Review

**As a** trainee,
**I want** to view my past assessment attempts and results,
**so that** I can track my improvement and review mistakes.

**Acceptance Criteria:**

1. Backend exposes `GET /api/topics/:topicId/assessments/:assessmentType/attempts` endpoint (requires Trainee role) returning all attempts for trainee with fields: attempt_number, started_at, submitted_at, score, passed, questions_snapshot (includes trainee's answers)
2. Frontend implements Assessment History page (route: `/topics/:topicId/assessments/:assessmentType/history`) showing table of attempts: attempt number, date, score, pass/fail status, "View Results" action
3. Frontend allows clicking "View Results" to navigate to Assessment Results page (Story 5.4) for that specific attempt
4. Frontend allows comparing attempts side-by-side (optional enhancement: show score trend chart)
5. Frontend displays attempt history link on Topic Content View page
6. Local testability: Trainee takes 3 KC attempts with different scores, views history showing all 3 attempts, clicks to review results of attempt 2

### Story 5.7: Assessment Configuration for Heads

**As a** Head of Training Center,
**I want** to configure attempt limits and passing thresholds per assessment type,
**so that** I can adjust difficulty and accountability based on program needs.

**Acceptance Criteria:**

1. Database migration creates `assessment_config` table with columns: id (UUID), assessment_type_id (FK to assessment_types), max_attempts (integer), passing_threshold_percentage (integer), questions_per_attempt (integer), created_at, updated_at
2. Database seeds default configuration: KC (max_attempts=3, passing_threshold=70, questions_per_attempt=20), MA (max_attempts=2, passing_threshold=75, questions_per_attempt=15)
3. Backend exposes `GET /api/admin/settings/assessment-config` endpoint (requires HeadOfTrainingCenter role) returning current configuration
4. Backend exposes `PATCH /api/admin/settings/assessment-config/:assessmentTypeId` endpoint (requires HeadOfTrainingCenter role) allowing updates to max_attempts, passing_threshold_percentage, questions_per_attempt
5. Backend validates configuration: max_attempts >= 1, passing_threshold between 0-100, questions_per_attempt > 0
6. Frontend implements Assessment Configuration page (route: `/admin/settings/assessments`) accessible only to HeadOfTrainingCenter with form fields for each assessment type showing current values and allowing edits
7. Frontend displays warning when changing configuration: "This will affect all future assessment attempts. Existing attempts are unaffected."
8. Frontend allows configuring per-cohort or per-specialization assessment config (optional enhancement, defer to post-MVP if complex)
9. Local testability: Admin changes KC max_attempts to 5 and passing_threshold to 80%, saves configuration, verifies new trainees subject to new limits

---

## Epic 6: Lab Submission & TA Grading Workflow

**Goal:** Build lab assignment creation by trainers, trainee submission workflows (GitHub repository links and file uploads), TA-mentee assignment system, rubric-based grading interface, feedback delivery, and repository snapshots to prevent post-submission changes. This epic completes the hands-on assessment workflow, enabling practical skills evaluation.

### Story 6.1: Lab Assignment Data Model and Creation

**As a** Trainer,
**I want** to create lab assignments for modules with descriptions, requirements, and rubrics,
**so that** trainees understand expectations for practical work.

**Acceptance Criteria:**

1. Database migration creates `lab_assignments` table with columns: id (UUID), module_id (FK to modules), title (text), description (text, rich text HTML), requirements (text, rich text HTML), due_date (date, nullable), max_score (integer, default 100), created_by_user_id (FK to users), created_at, updated_at
2. Database migration creates `lab_rubric_items` table with columns: id (UUID), lab_assignment_id (FK to lab_assignments), criterion (text, e.g., "Code Quality"), description (text), max_points (integer), sequence_order (integer), created_at
3. Backend exposes `POST /api/modules/:moduleId/labs` endpoint (requires Trainer role with specialization access) creating lab assignment with title, description, requirements, rubric_items (array)
4. Backend validates rubric_items: sum of max_points across all items must equal max_score (default 100)
5. Backend exposes `GET /api/modules/:moduleId/labs` endpoint (authenticated users) returning all lab assignments for a module
6. Backend exposes `PATCH /api/labs/:id` endpoint (requires Trainer role) updating lab details and rubric
7. Backend exposes `DELETE /api/labs/:id` endpoint (requires Trainer role) soft-deleting lab assignment
8. Frontend implements Lab Assignment Editor page (route: `/modules/:moduleId/labs/new`) with form fields: title, description (rich text), requirements (rich text), due date (date picker), rubric items (dynamic list allowing add/remove rows with criterion, description, max_points)
9. Frontend validates rubric totals to 100 points before allowing save
10. Frontend displays lab assignments on Module Detail page visible to all users
11. Local testability: Trainer creates lab "Build REST API" with 5 rubric criteria totaling 100 points, saves, verifies lab appears on module page

### Story 6.2: TA-Mentee Assignment System

**As a** Head of Chapter,
**I want** to assign TAs to specific trainees for mentorship and grading,
**so that** each trainee has a dedicated TA for personalized feedback.

**Acceptance Criteria:**

1. Database migration creates `ta_mentee_assignments` table with columns: id (UUID), ta_user_id (FK to users, must be TA role), mentee_user_id (FK to users, must be Trainee role), specialization_id (FK to specializations), cohort_id (FK to cohorts), assigned_at (timestamp), created_at
2. Database creates unique constraint on (ta_user_id, mentee_user_id, specialization_id, cohort_id) to prevent duplicate assignments
3. Backend exposes `POST /api/admin/ta-assignments` endpoint (requires HeadOfChapter or HeadOfTrainingCenter role) accepting ta_user_id, mentee_user_ids (array), specialization_id, cohort_id
4. Backend validates: ta_user_id has TA role and is assigned to specialization; mentee_user_ids are Trainees in the cohort
5. Backend inserts records into `ta_mentee_assignments` for each mentee
6. Backend exposes `GET /api/admin/specializations/:specializationId/ta-assignments` endpoint returning TA-mentee pairings for specialization with TA name, mentee names, cohort
7. Backend exposes `GET /api/tas/me/mentees` endpoint (requires TA role) returning list of assigned mentees with profiles: name, cohort, specialization, progress summary
8. Frontend implements TA Assignment page (route: `/admin/specializations/:specializationId/ta-assignments`) accessible to HeadOfChapter showing current assignments with ability to add/remove pairings
9. Frontend allows bulk assignment: upload CSV with columns (TA email, Mentee email), system matches emails to user IDs and creates assignments
10. Frontend displays TA's mentees on TA Dashboard with quick access to mentee profiles
11. Local testability: Admin assigns TA "Alice" to mentees "Bob" and "Charlie" in Backend specialization, verifies assignments visible on admin page and TA's dashboard

### Story 6.3: Lab Submission - GitHub Repository Link (Primary Method)

**As a** trainee,
**I want** to submit my lab by providing a GitHub repository link,
**so that** my TA can review my code in its natural development environment.

**Acceptance Criteria:**

1. Database migration creates `lab_submissions` table with columns: id (UUID), lab_assignment_id (FK to lab_assignments), trainee_id (FK to users), submission_type (enum: github_link, file_upload), github_url (text, nullable), snapshot_url (text, nullable, for archived repo state), submitted_at (timestamp), graded_by_user_id (FK to users, nullable), grade (integer, nullable), feedback (text, nullable), graded_at (timestamp, nullable), created_at, updated_at
2. Backend exposes `POST /api/labs/:labId/submit` endpoint (requires Trainee role) accepting submission_type and github_url (if type=github_link)
3. Endpoint validates GitHub URL format: must be valid URL matching pattern `https://github.com/{user}/{repo}`
4. Endpoint checks repository visibility by making HEAD request to GitHub URL; if returns 404, return error "Repository not found or not public. Ensure your repository is public."
5. Endpoint archives repository state by triggering background job (Bull) to clone repository and store snapshot in Azure Blob Storage; stores snapshot_url in lab_submissions
6. Endpoint checks for existing submission: if trainee already submitted this lab, return error "Lab already submitted. Resubmissions not allowed."
7. Endpoint inserts `lab_submissions` record with submission_type=github_link, github_url, submitted_at=now
8. Endpoint updates `trainee_progress` if lab submission completes module requirements (all topics completed + lab submitted)
9. Frontend implements Lab Submission page (route: `/labs/:labId/submit`) with form: submission method radio buttons (GitHub Link, File Upload), GitHub URL input field (if GitHub selected), file upload input (if File Upload selected), "Submit Lab" button
10. Frontend displays confirmation modal: "Are you sure? You cannot resubmit after final submission."
11. Frontend displays success message after submission: "Lab submitted successfully! Your TA will review it soon."
12. Frontend displays loading indicator during repository snapshot job: "Archiving repository snapshot..." with progress updates via job status polling
13. Local testability: Trainee submits lab with GitHub URL, verifies submission record created, repository snapshot job completes, snapshot_url stored

### Story 6.4: Lab Submission - File Upload (Secondary Method)

**As a** trainee,
**I want** to submit my lab by uploading files directly,
**so that** I can submit work even if I don't use GitHub.

**Acceptance Criteria:**

1. Backend updates `POST /api/labs/:labId/submit` endpoint to accept submission_type=file_upload with multipart file upload (multiple files allowed, max 50MB total)
2. Endpoint validates file types: allow code files (common extensions: .js, .py, .java, .html, .css, etc.), documents (.pdf, .docx), zip archives (.zip, .tar.gz)
3. Endpoint uploads files to Azure Blob Storage with naming convention: `lab-submissions/{labId}/{traineeId}/{filename}`
4. Endpoint stores file metadata: insert into `lab_submission_files` table with columns: id (UUID), lab_submission_id (FK to lab_submissions), file_name, file_type, storage_url, created_at
5. Endpoint inserts `lab_submissions` record with submission_type=file_upload, snapshot_url referencing Azure Blob container path
6. Frontend allows multiple file selection or drag-and-drop upload on Lab Submission page
7. Frontend displays upload progress bar for each file
8. Frontend lists uploaded files with file name, size, and remove button (before final submission)
9. Frontend enforces 50MB total upload size limit with validation error if exceeded
10. Local testability: Trainee uploads 3 code files totaling 10MB, submits lab, verifies files stored in Azure Blob, submission record created with file metadata

### Story 6.5: TA Grading Queue and Lab Review Interface

**As a** TA,
**I want** a queue of pending lab submissions from my mentees,
**so that** I can efficiently prioritize and grade labs.

**Acceptance Criteria:**

1. Backend exposes `GET /api/tas/me/grading-queue` endpoint (requires TA role) returning pending lab submissions from TA's assigned mentees (graded_at IS NULL) with details: submission_id, trainee_name, lab_title, module_name, submitted_at, days_since_submission
2. Backend sorts queue by submitted_at (oldest first) to prioritize long-pending labs
3. Backend exposes `GET /api/lab-submissions/:id` endpoint (requires TA role, validates TA assigned to mentee) returning full submission details: lab assignment (title, description, requirements, rubric), submission files or github_url, trainee profile
4. Frontend implements TA Grading Queue page (route: `/ta/grading-queue`) displaying card-based layout of pending labs with: trainee name, lab title, submitted date, "Grade Now" button
5. Frontend highlights overdue labs (submitted >48 hours ago) with red border or badge
6. Frontend allows filtering queue by specialization, module, or trainee
7. Frontend implements Lab Review Interface (route: `/ta/grade/:submissionId`) with split-pane layout:
   - Left pane: Lab requirements, rubric items as checklist/scorecard
   - Right pane: Submitted code preview (if GitHub link, embed GitHub UI via iframe or fetch files; if uploaded files, display file tree with syntax-highlighted code viewer)
8. Frontend allows inline commenting on code (optional enhancement, defer if complex)
9. Local testability: TA views grading queue showing 3 pending labs from mentees, clicks "Grade Now" on first lab, views lab requirements and submitted GitHub repository

### Story 6.6: Rubric-Based Grading and Feedback Submission

**As a** TA,
**I want** to grade labs using the rubric and provide written feedback,
**so that** trainees receive structured, actionable feedback.

**Acceptance Criteria:**

1. Backend exposes `POST /api/lab-submissions/:id/grade` endpoint (requires TA role, validates TA assigned to mentee) accepting: rubric_scores (array of {rubric_item_id, points_awarded}), overall_grade (calculated from rubric), feedback (text, required)
2. Endpoint validates rubric_scores: points_awarded <= max_points for each rubric item
3. Endpoint calculates overall_grade = sum of points_awarded across all rubric items
4. Endpoint updates `lab_submissions` record: grade=overall_grade, feedback, graded_by_user_id=TA, graded_at=now
5. Endpoint inserts `lab_rubric_scores` records (new table) with columns: id (UUID), lab_submission_id, rubric_item_id, points_awarded, created_at
6. Endpoint triggers email notification to trainee: subject "Your lab has been graded: [Lab Title]" with body including grade, feedback, link to view full results
7. Frontend displays rubric scorecard in Lab Review Interface: each rubric criterion with slider or input field to assign points (0 to max_points)
8. Frontend displays real-time grade calculation as TA assigns points: "Total Score: 85/100"
9. Frontend includes required feedback textarea (minimum 50 characters) with placeholder: "Provide constructive feedback on strengths and areas for improvement..."
10. Frontend validates all rubric items scored before allowing submission
11. Frontend displays confirmation modal: "Submit grade? You cannot change the grade after submission."
12. Frontend displays success message after grading: "Lab graded successfully. Notification sent to trainee."
13. Local testability: TA grades lab by assigning points to each rubric item (totaling 85/100), writes feedback, submits grade, verifies grade and feedback saved, trainee receives email notification

### Story 6.7: Trainee Lab Results and Feedback View

**As a** trainee,
**I want** to view my graded lab results with detailed rubric scores and TA feedback,
**so that** I can understand my strengths and areas for improvement.

**Acceptance Criteria:**

1. Backend exposes `GET /api/labs/:labId/my-submission` endpoint (requires Trainee role) returning trainee's submission with grading details: overall_grade, rubric_scores (array of {criterion, points_awarded, max_points}), feedback, graded_at, graded_by (TA name)
2. Frontend implements Lab Results page (route: `/labs/:labId/results`) displaying:
   - Header: "Lab Grade: 85/100" with pass/fail indicator (if passing grade defined, e.g., >70)
   - Rubric breakdown table: criterion, points awarded, max points, performance (e.g., "7/10 - Good")
   - TA feedback section: "Feedback from [TA Name]" with formatted text feedback
   - Graded date: "Graded on [Date]"
3. Frontend displays lab results link on trainee dashboard after lab graded
4. Frontend sends in-app notification badge when lab graded (notification center integration)
5. Frontend allows trainee to download graded lab report as PDF (optional enhancement)
6. Local testability: Trainee views lab results showing rubric scores and TA feedback, verifies overall grade matches rubric total

---

## Epic 7: Analytics, Performance Metrics & Employment Decisions

**Goal:** Implement automated performance metric calculations, role-specific analytics dashboards for Heads, configurable evaluation thresholds per cohort and specialization, at-risk trainee identification, and the three-level employment decision workflow with comprehensive audit trails. This epic delivers data-driven decision-making tools for leadership.

### Story 7.1: Performance Metrics Calculation Engine

**As a** system,
**I want** to automatically calculate trainee performance metrics,
**so that** leadership can make data-driven employment decisions.

**Acceptance Criteria:**

1. Database migration creates `trainee_performance_metrics` table with columns: id (UUID), trainee_id (FK to users), cohort_id (FK to cohorts), kc_average (float), ma_average (float), lab_average (float), overall_technical_score (float), completion_rate (float), on_time_rate (float), improvement_trend (enum: improving, stable, declining, insufficient_data), calculated_at (timestamp), created_at
2. Backend implements scheduled job (Bull queue) running nightly calculating metrics for all active trainees
3. Job queries assessment attempts: calculate kc_average = average of all passed KC scores per trainee, ma_average = average of all passed MA scores
4. Job queries lab submissions: calculate lab_average = average of all graded lab scores
5. Job calculates overall_technical_score = weighted average: (kc_average * 0.20) + (ma_average * 0.40) + (lab_average * 0.40) (weights configurable via environment variables)
6. Job calculates completion_rate = (completed topics / total topics in specialization) * 100
7. Job calculates on_time_rate = (modules completed on-time / total modules with deadlines) * 100
8. Job calculates improvement_trend by comparing current month's average scores to previous month; if increase >5%, mark improving; if decrease >5%, mark declining; else stable; if <2 months data, insufficient_data
9. Job inserts/updates `trainee_performance_metrics` record with calculated_at=now
10. Backend exposes `GET /api/trainees/:id/performance` endpoint (requires Head roles or trainee self) returning latest performance metrics
11. Unit tests cover metric calculation logic with sample data
12. Local testability: Developer triggers metric calculation job manually, verifies metrics calculated correctly for test trainee with known scores

### Story 7.2: Monthly Performance Snapshots for Audit Trail

**As a** Head of Training Center,
**I want** monthly snapshots of trainee performance,
**so that** I have historical data for employment decisions and audit compliance.

**Acceptance Criteria:**

1. Database migration creates `performance_snapshots` table with columns: id (UUID), trainee_id (FK to users), cohort_id (FK to cohorts), snapshot_date (date), kc_average, ma_average, lab_average, overall_technical_score, completion_rate, on_time_rate, improvement_trend, created_at
2. Backend implements scheduled job running on 1st of each month creating snapshot records for all active trainees by copying current metrics from `trainee_performance_metrics` to `performance_snapshots`
3. Job sets snapshot_date to last day of previous month (e.g., run on Feb 1 creates snapshot for Jan 31)
4. Backend exposes `GET /api/trainees/:id/performance/history` endpoint (requires Head roles) returning all snapshots for trainee ordered by snapshot_date descending
5. Frontend implements Performance History page (route: `/trainees/:id/performance/history`) displaying table of monthly snapshots with trend charts (line graphs showing score trends over time)
6. Frontend allows exporting performance history as CSV
7. Local testability: Developer manually triggers snapshot job, verifies snapshot records created with correct snapshot_date, views performance history showing multiple months

### Story 7.3: Configurable Evaluation Thresholds

**As a** Head of Training Center,
**I want** to configure minimum performance thresholds per cohort and specialization,
**so that** employment decisions reflect program-specific standards.

**Acceptance Criteria:**

1. Database migration creates `evaluation_thresholds` table with columns: id (UUID), cohort_id (FK to cohorts), specialization_id (FK to specializations, nullable for cohort-wide), min_kc_percentage (integer), min_ma_percentage (integer), min_lab_percentage (integer), min_completion_rate (integer), min_on_time_rate (integer), created_at, updated_at, created_by_user_id (FK to users)
2. Backend exposes `POST /api/admin/cohorts/:cohortId/thresholds` endpoint (requires HeadOfProgram or HeadOfTrainingCenter role) creating threshold configuration
3. Backend exposes `GET /api/cohorts/:cohortId/thresholds` endpoint returning thresholds with specialization breakdown
4. Backend exposes `PATCH /api/admin/thresholds/:id` endpoint updating threshold values (only by Heads of Program or Training Center)
5. Backend validates thresholds: all percentage values between 0-100
6. Backend allows both cohort-wide thresholds (specialization_id NULL) and specialization-specific overrides (specialization_id set)
7. Frontend implements Threshold Configuration page (route: `/admin/cohorts/:cohortId/thresholds`) showing table of specializations with threshold input fields per metric
8. Frontend allows copying thresholds from another cohort (template functionality)
9. Frontend displays warning if thresholds set very high (e.g., >90%) or very low (e.g., <50%): "This threshold may be too strict/lenient"
10. Local testability: Admin sets thresholds for Backend specialization in GTP 2026 Q1: min_kc=70, min_ma=75, min_lab=80, min_completion=90, min_on_time=70; verifies saved correctly

### Story 7.4: At-Risk Trainee Identification and Alerts

**As a** Head of Program,
**I want** to automatically identify trainees falling below thresholds,
**so that** I can intervene early to support struggling trainees.

**Acceptance Criteria:**

1. Backend implements scheduled job (nightly, after metrics calculation) identifying at-risk trainees by comparing `trainee_performance_metrics` against `evaluation_thresholds` for their cohort and specialization
2. Job flags trainee as at-risk if ANY metric falls below corresponding threshold (e.g., kc_average < min_kc_percentage)
3. Database migration adds `at_risk_flag` (boolean) column to `trainee_performance_metrics` table; job updates this flag
4. Backend exposes `GET /api/cohorts/:cohortId/at-risk-trainees` endpoint (requires Head roles) returning list of flagged trainees with: name, specialization, failed metrics (which thresholds not met), current values
5. Backend sends weekly email digest to Head of Program and Head of Training Center listing at-risk trainees
6. Frontend implements At-Risk Trainees page (route: `/cohorts/:cohortId/at-risk`) displaying table with trainee name, specialization, red flags (metrics below threshold highlighted), actions (view profile, contact)
7. Frontend highlights at-risk trainees on Head dashboards with red warning icons
8. Frontend allows filtering at-risk list by specialization, severity (1 metric failed vs. multiple), improvement trend
9. Local testability: Developer creates test trainee with scores below thresholds, runs at-risk job, verifies trainee flagged, appears on at-risk list, email digest includes trainee

### Story 7.5: Head of Chapter, Program, and Training Center Dashboards

**As a** Head of Chapter, Program, or Training Center,
**I want** role-specific analytics dashboards,
**so that** I can monitor cohort performance and make informed decisions.

**Acceptance Criteria:**

1. **Head of Chapter Dashboard (route: `/dashboards/chapter/:specializationId`)**:
   - Displays chapter-wide analytics: trainee count, average performance metrics (KC, MA, Lab), topic difficulty heatmap (topics with high failure rates)
   - Shows trainer and TA assignments with workload (mentees per TA)
   - Shows question approval queue count with link to pending reviews
   - Displays at-risk trainees in chapter with quick actions
2. **Head of Program Dashboard (route: `/dashboards/program/:cohortId`)**:
   - Displays cohort overview: total trainees, completion rates by specialization (bar chart), average scores by specialization (comparison table)
   - Shows timeline progress: percentage of cohort on-track vs. behind on deadlines
   - Shows at-risk trainee count with drill-down link
   - Displays employment readiness summary: trainees meeting thresholds vs. not meeting
3. **Head of Training Center Dashboard (route: `/dashboards/training-center`)**:
   - Displays system-wide analytics: all cohorts, all specializations, total trainees, overall completion rates
   - Shows cohort comparison: side-by-side metrics for GTP vs. NSP programs
   - Shows user management summary: total users by role, recent additions
   - Shows system health: recent audit log activity, data integrity checks
4. Backend exposes dedicated analytics endpoints per role:
   - `GET /api/analytics/chapter/:specializationId` for HeadOfChapter
   - `GET /api/analytics/program/:cohortId` for HeadOfProgram
   - `GET /api/analytics/training-center` for HeadOfTrainingCenter
5. Frontend implements data visualizations using charting library (Chart.js, Recharts): bar charts, line graphs, pie charts for metric distributions
6. Frontend allows date range filtering: view analytics for last 30 days, 90 days, or all-time
7. Frontend allows exporting dashboard data as PDF or Excel
8. Local testability: Head of Program logs in, views dashboard showing cohort analytics with charts, verifies data matches database queries

### Story 7.6: Three-Level Employment Decision Workflow

**As a** Head of Chapter, Program, and Training Center,
**I want** a structured three-level review workflow for employment decisions,
**so that** decisions are collaborative, documented, and defensible.

**Acceptance Criteria:**

1. Database migration creates `employment_decisions` table with columns: id (UUID), trainee_id (FK to users), cohort_id (FK to cohorts), chapter_head_notes (text, nullable), chapter_head_reviewed_at (timestamp, nullable), chapter_head_user_id (FK to users, nullable), program_head_recommendation (enum: hire, conditional_hire, no_offer, nullable), program_head_notes (text, nullable), program_head_reviewed_at (timestamp, nullable), program_head_user_id (FK to users, nullable), final_decision (enum: hire, conditional_hire, no_offer, nullable), final_decision_notes (text, nullable), final_decision_at (timestamp, nullable), final_decision_user_id (FK to users, nullable), created_at, updated_at
2. Database migration creates `employment_decision_audit` table with columns: id (UUID), employment_decision_id (FK to employment_decisions), action (enum: created, chapter_reviewed, program_recommended, final_decided), performed_by_user_id (FK to users), notes (text), performed_at (timestamp), created_at
3. Backend exposes `POST /api/cohorts/:cohortId/employment-decisions/initiate` endpoint (requires HeadOfChapter role) creating employment_decision records for all trainees in cohort eligible for review (completed program or reached decision milestone)
4. Backend exposes `GET /api/employment-decisions/:id` endpoint (requires Head roles) returning decision record with all review levels, trainee performance summary, soft skills score
5. Backend exposes `PATCH /api/employment-decisions/:id/chapter-review` endpoint (requires HeadOfChapter role) accepting chapter_head_notes; updates chapter_head fields and logs audit record
6. Backend exposes `PATCH /api/employment-decisions/:id/program-recommendation` endpoint (requires HeadOfProgram role) accepting program_head_recommendation and program_head_notes; updates program_head fields and logs audit record
7. Backend exposes `PATCH /api/employment-decisions/:id/final-decision` endpoint (requires HeadOfTrainingCenter role) accepting final_decision and final_decision_notes; updates final_decision fields, logs audit record, marks decision as complete
8. Frontend implements Employment Decision Workflow page (route: `/employment-decisions/:id`) with stepper UI showing three levels: Chapter Review → Program Recommendation → Final Decision
9. Frontend displays trainee performance summary card: all metrics, threshold comparison, at-risk flags, soft skills score input field (manual entry by Heads)
10. Frontend displays form fields for current user's review level (e.g., if Head of Chapter viewing, show chapter_head_notes textarea and "Submit Chapter Review" button)
11. Frontend displays read-only previous review levels if already completed (e.g., show chapter notes if on program recommendation step)
12. Frontend prevents out-of-order reviews: Program Head cannot recommend until Chapter Head reviewed; Training Center Head cannot finalize until Program Head recommended
13. Frontend displays audit log timeline showing all actions with timestamps and users
14. Local testability: HeadOfChapter submits review notes for trainee, HeadOfProgram views trainee and submits recommendation, HeadOfTrainingCenter views trainee and submits final decision, verifies all steps logged in audit table

### Story 7.7: Employment Decision Export and Reporting

**As a** Head of Training Center,
**I want** to export employment decisions with performance data,
**so that** I can provide documentation to HR and senior leadership.

**Acceptance Criteria:**

1. Backend exposes `GET /api/cohorts/:cohortId/employment-decisions/export` endpoint (requires HeadOfTrainingCenter role) generating report file (PDF or Excel)
2. Report includes: cohort name, date range, list of trainees with columns: name, specialization, technical score, soft skills score, completion rate, on-time rate, chapter notes summary, program recommendation, final decision
3. Report highlights trainees receiving offers (hire, conditional_hire) vs. no offers
4. Report includes summary statistics: total trainees, hire rate, average scores of hired trainees
5. Report footer includes generation date, generated by user name, and disclaimer: "This report is confidential and for internal use only"
6. Frontend implements Export button on Employment Decisions list page triggering download
7. Frontend allows filtering export: all trainees, only hired, only not hired
8. Local testability: Admin exports employment decisions for cohort, downloads PDF, verifies all trainee data included with correct final decisions

---

## Checklist Results Report

### Executive Summary

**Overall PRD Completeness:** 85% - Strong foundation with minor gaps

**MVP Scope Appropriateness:** Just Right - 7 epics deliver complete training lifecycle in logical sequence without over-engineering

**Readiness for Architecture Phase:** **Ready with Minor Refinements** - PRD provides sufficient detail for architecture design to begin; identified gaps are non-blocking and can be addressed during architecture phase

**Most Critical Strengths:**
- Comprehensive functional requirements (63 FRs) covering all core workflows
- Well-structured epic/story breakdown with clear dependencies and sequencing
- Detailed acceptance criteria enabling immediate development kickoff
- Strong technical guidance with explicit technology stack and architecture decisions
- Excellent balance of "what" vs "how" - requirements focus on outcomes, not implementation

**Most Critical Gaps:**
1. MVP validation approach undefined (success criteria, feedback mechanisms, iteration plan)
2. Data quality standards and retention policies not specified
3. Support and operational runbooks not defined
4. Stakeholder approval process not documented

**Recommendation:** **PROCEED TO ARCHITECTURE PHASE** - The identified gaps are process/operational concerns that can be addressed in parallel with architecture work. The PRD provides sufficient technical clarity for the architect to begin detailed design.

---

### Category Analysis

| Category                         | Status    | Critical Issues |
| -------------------------------- | --------- | --------------- |
| 1. Problem Definition & Context  | PASS      | None - Goals and Background Context clearly articulate problem and quantify impact |
| 2. MVP Scope Definition          | PARTIAL   | Missing: Explicit out-of-scope section, MVP validation approach, success criteria for moving beyond MVP |
| 3. User Experience Requirements  | PASS      | Comprehensive UI Design Goals section; detailed screen descriptions; accessibility requirements clear |
| 4. Functional Requirements       | PASS      | Excellent - 63 FRs with clear, testable specifications |
| 5. Non-Functional Requirements   | PARTIAL   | Missing: Security testing requirements, detailed resource utilization constraints, data quality standards |
| 6. Epic & Story Structure        | PASS      | Outstanding - logical sequencing, appropriate sizing, comprehensive acceptance criteria |
| 7. Technical Guidance            | PASS      | Strong architecture direction with rationale; missing: explicit technical debt approach |
| 8. Cross-Functional Requirements | PARTIAL   | Missing: Data retention policies, API documentation standards, support/operational requirements |
| 9. Clarity & Communication       | PASS      | Well-written, structured, and versioned; missing: stakeholder approval process |

---

### Top Issues by Priority

#### BLOCKERS: None

All critical requirements for architecture phase are documented.

#### HIGH PRIORITY (Should Address Before Development Kickoff)

1. **MVP Validation Approach (Section 2.3 gap)**
   - **Issue:** No defined method for validating MVP success post-launch
   - **Impact:** Risk of building features without clear validation criteria
   - **Recommendation:** Add section defining pilot cohort approach, UAT process with training staff, feedback collection mechanisms, and criteria for declaring MVP successful
   - **Blocking:** Development? No. Architecture? No.

2. **Data Quality & Retention Policies (Section 8.1 gap)**
   - **Issue:** No standards for data validation, cleansing, or retention periods beyond "30-day backup retention"
   - **Impact:** Potential compliance risk for employment decision data; unclear audit log retention
   - **Recommendation:** Define retention policy for audit logs (recommend 7 years for employment decisions), performance snapshots (indefinite?), assessment attempts (2 years post-graduation?)
   - **Blocking:** Development? Not initially. Architecture? Schema design may need consideration.

3. **Support & Operational Requirements (Section 8.3 gap)**
   - **Issue:** No definition of support model (who supports system?), SLA for issue resolution, runbook requirements
   - **Impact:** Post-launch operational readiness unclear
   - **Recommendation:** Define support ownership (DevOps team? BMAD team?), incident response procedures, runbook requirements per epic
   - **Blocking:** Development? No. Architecture? Monitoring/alerting design should consider support needs.

#### MEDIUM PRIORITY (Would Improve Clarity)

4. **Explicit Out-of-Scope Section**
   - **Issue:** Out-of-scope items referenced in Project Brief not repeated in PRD
   - **Impact:** Potential scope creep during development
   - **Recommendation:** Add "Out of Scope for MVP" section after Epic List listing: mobile native apps, discussion forums, real-time chat, video conferencing, automated code quality analysis, predictive analytics, gamification, peer review, multi-language support, external integrations
   - **Blocking:** No, but would prevent stakeholder confusion

5. **Security Testing Requirements**
   - **Issue:** NFR mentions security features (encryption, RBAC) but no security testing requirements
   - **Impact:** Security vulnerabilities may not be discovered pre-launch
   - **Recommendation:** Add to Testing Requirements: penetration testing before production launch, OWASP Top 10 vulnerability scanning in CI/CD, security code review for authentication/authorization logic
   - **Blocking:** No, can be added to Epic 1 Story 1.7 (CI/CD)

6. **Technical Debt Approach**
   - **Issue:** No guidance on acceptable technical debt during MVP vs. post-MVP refactoring
   - **Impact:** Developers may over-engineer or under-engineer without clear guidance
   - **Recommendation:** Add principle: "Accept technical debt for MVP speed if: (1) doesn't compromise security/data integrity, (2) doesn't block core workflows, (3) documented in code comments for post-MVP refactoring"
   - **Blocking:** No, but would improve development velocity

7. **API Documentation Standards**
   - **Issue:** OpenAPI/Swagger mentioned but no standard for request/response documentation
   - **Impact:** Frontend-backend integration friction
   - **Recommendation:** Add to Epic 1: API documentation required for all endpoints using OpenAPI 3.0 spec, auto-generated from code annotations, published to internal docs site
   - **Blocking:** No, can be established during Epic 1

#### LOW PRIORITY (Nice to Have)

8. **Stakeholder Approval Process**
   - **Issue:** No documented process for PRD approval, change request handling during development
   - **Impact:** Unclear decision authority for mid-stream changes
   - **Recommendation:** Define approval workflow (PM presents to Head of Training Center → approval documented in change log), change request process (PM evaluates impact, Head of Training Center approves scope changes)
   - **Blocking:** No, operational process issue

9. **Competitive Analysis in PRD**
   - **Issue:** Project Brief mentions LMS comparison but PRD doesn't include competitive landscape
   - **Impact:** None for development; may miss UX best practices
   - **Recommendation:** UX Expert phase should include competitive analysis (Canvas LMS, Coursera for Business) for UI/UX patterns
   - **Blocking:** No, deferred to UX phase appropriately

10. **Detailed User Personas**
    - **Issue:** Roles defined but not full persona profiles (motivations, frustrations, technical proficiency)
    - **Impact:** Minimal - roles and needs sufficiently clear for development
    - **Recommendation:** UX Expert can create detailed personas during design phase if needed
    - **Blocking:** No

---

### MVP Scope Assessment

**Features That Could Be Cut for True MVP:**

The current scope is well-balanced. Potential simplifications if timeline risk emerges:

1. **Epic 4 Story 4.6 (Question Performance Analytics):** Could defer detailed analytics to post-MVP; manually review flagged questions instead of automated flagging
2. **Epic 7 Story 7.2 (Monthly Performance Snapshots):** Could simplify to only store final snapshot at employment decision time instead of monthly
3. **Notification customization (FR55):** Could default all notifications to enabled without trainee preferences toggle for MVP

**Recommendation:** **Do not cut these features.** The current 7-epic scope is already minimal for delivering a viable system that replaces manual processes. Cutting further risks delivering incomplete workflows that won't achieve adoption goals.

**Missing Features That Are Essential:**

None identified. The PRD comprehensively covers the training lifecycle based on Project Brief requirements.

**Complexity Concerns:**

1. **Epic 4 (AI Question Generation):** Highest technical risk due to AI API dependencies, prompt engineering iteration needs, and quality control requirements. Mitigation: Story 4.2 includes background job pattern to avoid blocking; Story 4.3 provides manual review workflow as safety net.

2. **Epic 7 (Employment Decisions):** Complex three-level workflow with audit requirements. Mitigation: Stories break down into manageable pieces; audit logging established early in Epic 1.

3. **Integration Dependencies:** Microsoft SSO (Epic 1), AI APIs (Epic 4), Azure services (multiple epics) create external dependencies. Mitigation: Stories include validation steps and error handling; Epic 1 establishes integration patterns early.

**Timeline Realism:**

**6-month MVP timeline is aggressive but achievable with conditions:**

- **Team size assumption:** 3-4 developers (1 backend, 1 frontend, 1 full-stack, 1 QA) as stated in Project Brief
- **Velocity assumption:** ~3-4 stories per developer per 2-week sprint = ~24-32 stories per sprint for team
- **Total stories:** 47 stories across 7 epics
- **Estimated sprints:** ~12 sprints (24 weeks / 6 months) = ~4 stories per sprint required
- **Buffer:** Minimal buffer for unknowns (AI integration iteration, UAT feedback)

**Risks to timeline:**
- AI question generation quality iteration (Epic 4) may take 2-3 sprints instead of 1
- Microsoft SSO integration may have company IT approval delays
- UAT feedback may require rework

**Recommendation:** **Plan for 7-month delivery (1 month buffer)** to de-risk timeline, or **descope Epic 7 Stories 7.5-7.7 (detailed analytics dashboards)** to 8-month post-MVP delivery, keeping core employment decision workflow (Stories 7.1-7.4, 7.6) in MVP.

---

### Technical Readiness

**Clarity of Technical Constraints:** Excellent

- Technology stack explicitly defined (React, Node.js/Express, PostgreSQL, Redis, Azure)
- Architecture approach clear (monorepo, monolithic backend, RESTful API)
- Integration requirements detailed (Microsoft SSO OAuth 2.0, AI APIs, Azure Blob)
- Non-functional requirements quantified (performance, availability, security)

**Identified Technical Risks:**

1. **AI API Rate Limits & Costs**
   - **Risk:** OpenAI/Claude API calls for question generation may hit rate limits or exceed budget during bulk generation
   - **Mitigation in PRD:** Story 4.2 uses background job pattern; NFR14 requires graceful handling
   - **Architect TODO:** Design rate limiting and retry logic; cost estimation model per topic

2. **GitHub Repository Snapshot Complexity**
   - **Risk:** Cloning and archiving repositories at submission time may be slow or fail for large repos
   - **Mitigation in PRD:** Story 6.3 uses background job; validates public repo accessibility
   - **Architect TODO:** Define timeout limits (e.g., max repo size 500MB, 5-minute timeout), error handling for failed clones

3. **Microsoft SSO Integration Approval**
   - **Risk:** Company IT may require security review or custom configuration for Azure AD app registration
   - **Mitigation in PRD:** Epic 1 Story 1.3 includes local dev and production redirect URIs
   - **Architect TODO:** Coordinate with IT early; document required permissions (email, profile read)

4. **Database Schema Complexity**
   - **Risk:** 20+ tables with many relationships may create migration challenges
   - **Mitigation in PRD:** Stories define schema incrementally per epic; migration tooling established in Epic 1 Story 1.2
   - **Architect TODO:** Design ERD with normalization vs. performance trade-offs; index strategy for performance

5. **Performance Under Load**
   - **Risk:** 100+ concurrent users during assessment periods may strain database queries (e.g., question randomization, performance metric calculation)
   - **Mitigation in PRD:** NFR4 requires no degradation; Story 1.2 includes Redis caching; testing strategy includes load testing
   - **Architect TODO:** Database indexing strategy, caching strategy for read-heavy queries (dashboards, question pools)

**Areas Needing Architect Investigation:**

1. **Database Indexing Strategy:** PRD mentions indexes in some stories but comprehensive indexing plan needed for performance
2. **Caching Strategy:** Redis mentioned for sessions and performance metrics but detailed caching layers need design (API responses, question pools, dashboard data)
3. **File Storage Organization:** Azure Blob Storage for labs and assets—needs folder structure design, access control (signed URLs), cost optimization (lifecycle policies)
4. **Background Job Queue Architecture:** Bull mentioned for AI generation, notifications, snapshots—needs worker pool sizing, failure handling, monitoring
5. **API Rate Limiting:** Not mentioned in PRD—needed to prevent abuse and ensure fair resource usage across users
6. **Database Backup & Disaster Recovery:** NFR10 mentions daily backups but architect needs to design backup strategy (full vs. incremental, point-in-time recovery)

---

### Recommendations

#### Immediate Actions (Before Architect Starts)

1. **Clarify MVP Success Criteria:** Define pilot cohort selection (20 trainees in 1 specialization?), UAT timeline (2 weeks post-Epic 7?), success metrics (trainer satisfaction survey >80%, zero data loss incidents)
 
2. **Define Data Retention Policy:** Document retention periods for audit logs (7 years), performance snapshots (indefinite), assessment attempts (2 years), lab submissions (indefinite), content versions (indefinite with archival after 1 year)

3. **Establish Stakeholder Approval Process:** Head of Training Center reviews and approves PRD; change requests during development evaluated by PM and approved by Head of Training Center

#### Actions During Architecture Phase

4. **Security Testing Requirements:** Architect to include security testing plan (penetration testing pre-launch, OWASP scanning in CI/CD, security code review for auth/authz)

5. **API Documentation Standards:** Architect to define OpenAPI 3.0 standard, auto-generation approach (code annotations), internal docs hosting

6. **Technical Debt Guidelines:** Architect to document acceptable technical debt for MVP (explicitly call out areas where "good enough" is acceptable for speed)

#### Actions During Development

7. **Support Model Definition:** By end of Epic 1, define support ownership, incident response SLA, runbook requirements per epic

8. **Out-of-Scope Communication:** PM to create stakeholder FAQ document listing out-of-scope features and rationale (prevents mid-stream scope creep)

---

### Final Decision

**✅ READY FOR ARCHITECT**

The PRD is comprehensive, properly structured, and provides sufficient detail for the architect to begin technical design. The identified gaps are minor and can be addressed in parallel with architecture work without blocking progress.

**Strengths that make this PRD ready:**
- Clear problem statement and quantified business goals
- Comprehensive functional and non-functional requirements
- Well-structured epic/story breakdown with logical sequencing
- Detailed acceptance criteria enabling testability
- Explicit technical constraints and architecture guidance
- Appropriate scope for 6-7 month MVP delivery

**Next Steps:**
1. PM addresses high-priority gaps (MVP validation approach, data retention policy) in PRD update (1 day)
2. Head of Training Center reviews and approves PRD (1 day)
3. Architect begins Technical Architecture Document creation per "Architect Prompt" in Next Steps section
4. UX Expert begins wireframe creation per "UX Expert Prompt" in Next Steps section
5. Development team onboarding scheduled for post-architecture approval (Week 3)

---

*Checklist validation completed: 2025-10-23 by PM Agent (John)*

---

## Next Steps

### UX Expert Prompt

You have received the Training Center Management System (TCMS) PRD (docs/prd.md) outlining a comprehensive platform for managing company training programs with AI-powered assessments and employment decision support.

**Your task:** Create detailed UX/UI specifications and wireframes for the TCMS system using the PRD's User Interface Design Goals section as your foundation. Focus on:

1. **Information Architecture:** Define navigation structure, user flows, and screen hierarchy for all 6 user roles (Trainee, TA, Trainer, Head of Chapter, Head of Program, Head of Training Center)
2. **Wireframes:** Create low-fidelity wireframes for critical screens identified in the PRD (dashboards, assessment taking, grading interface, employment decision workflow)
3. **Design System:** Define visual design language, component library (buttons, forms, cards, modals), color palette, typography, and spacing system aligned with Microsoft Fluent UI aesthetic
4. **Responsive Layouts:** Ensure designs work on desktop (1920px), tablet (768px), and graceful degradation for mobile phones
5. **Accessibility:** Validate WCAG 2.1 AA compliance in design decisions (contrast ratios, focus states, keyboard navigation patterns)

Collaborate with the Architect to ensure UI designs align with technical constraints and implementation feasibility. Deliver UX specifications document and wireframe set ready for developer handoff.

### Architect Prompt

You have received the Training Center Management System (TCMS) PRD (docs/prd.md) outlining a comprehensive platform for managing company training programs with AI-powered assessments and employment decision support.

**Your task:** Create a detailed Technical Architecture Document addressing:

1. **System Architecture:** Define high-level architecture (monorepo structure, monolithic backend with modular design, frontend-backend communication patterns), deployment architecture (Azure App Service, Azure Blob Storage, PostgreSQL, Redis), and scalability considerations
2. **Database Schema:** Design complete entity-relationship diagram (ERD) with all tables, columns, data types, relationships, indexes, and constraints based on PRD data models
3. **API Specifications:** Define RESTful API endpoints for all features (authentication, content management, assessments, labs, analytics) with request/response schemas, authentication/authorization requirements, and error handling
4. **AI Integration Architecture:** Design question generation workflow, prompt engineering strategy, AI API integration patterns, error handling for API failures, and cost optimization strategies
5. **Security Architecture:** Define authentication flow (Microsoft SSO OAuth 2.0), authorization patterns (RBAC implementation), data encryption strategy, audit logging system, and compliance considerations
6. **Testing Strategy:** Define unit, integration, E2E testing approaches, local testability requirements, CI/CD pipeline design, and quality gates
7. **Monitoring & Operations:** Define application monitoring (Azure Application Insights), error tracking (Sentry), performance metrics, alerting strategy, and backup/recovery procedures

Use the PRD's Technical Assumptions section as your foundation. Deliver a comprehensive architecture document ready for Epic 1 developer kickoff, including decision records documenting key architectural choices and trade-offs.

---

*End of PRD*
