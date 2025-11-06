
# Project Brief: Training Center Management System

**Project Name:** Training Center Management System (TCMS)
**Version:** 1.0
**Date:** 2025-10-23
**Prepared By:** Business Analyst Mary & BMAD Team

---

## Executive Summary

The Training Center Management System (TCMS) is a comprehensive platform for managing company training programs, content delivery, AI-powered assessments, and performance-based employment decisions. The system serves two primary training programs—Graduate Training Program (GTP, 6 months) and National Service Personnel Training (NSP, 12 months)—supporting approximately 100+ trainees annually across six technical specializations (Backend, Frontend, QA, UI/UX, Data Engineering, DevOps).

**Core Value Proposition:** TCMS enables self-paced learning with deadline accountability, scales assessment creation through AI, and provides data-driven insights for employment decisions while maintaining human oversight and fairness.

**Target Market:** Internal enterprise use for company training operations, with potential white-label opportunities for similar corporate training programs.

**Key Differentiator:** Flexible, self-paced learning model combined with AI-powered assessment generation and configurable employment decision frameworks—purpose-built for high-stakes technical training programs.

---

## Problem Statement

### Current State & Pain Points

The company's training center currently operates using **fragmented tools and manual processes**:

1. **Content Management:** Course materials scattered across Microsoft Loop with no structured curriculum management, version control, or trainee progress tracking
2. **Assessment Creation:** Trainers manually create hundreds of questions (Knowledge Checks, Module Assessments) per cohort—time-consuming, inconsistent difficulty, potential for repetition across cohorts
3. **Lab Grading:** TAs manually grade ~100 trainee lab submissions with inconsistent rubrics and delayed feedback
4. **Progress Tracking:** No centralized system to track trainee completion, scores, or deadline compliance—relies on spreadsheets and email
5. **Employment Decisions:** Performance data exists in silos; decision-makers lack unified dashboards and audit trails; criteria are informal and inconsistent

### Impact of the Problem

**Quantified:**
- Trainers spend estimated **20-30 hours per module** creating assessments manually (6 specializations × ~8 modules = ~1,000 trainer hours annually)
- TAs average **2-3 days turnaround** on lab grading due to queue management challenges
- Head of Training Center lacks real-time visibility into cohort performance—reports are weeks behind reality
- No historical data for curriculum improvement (which topics are hardest? which assessments are flawed?)

**Qualitative:**
- **Trainee frustration:** Unclear expectations, delayed feedback, no visibility into own progress
- **Unfairness risk:** Inconsistent assessment quality and grading standards jeopardize employment decisions
- **Scalability ceiling:** Current manual processes cannot support >100 trainees or new specializations
- **Quality degradation:** Trainers stretched thin result in copy-paste assessments and generic feedback

### Why Existing Solutions Fall Short

**Generic LMS platforms (Moodle, Canvas, Blackboard):**
- Not designed for self-paced learning with mandatory deadlines
- No AI assessment generation
- No employment decision frameworks
- Lack flexible role-based workflows (6 distinct personas)

**Code training platforms (LeetCode, Udemy for Business):**
- Focus on content consumption, not internal training program management
- No cohort/program management
- No integration with company authentication and workflows
- Cannot migrate existing content from Microsoft Loop

**Custom spreadsheet solutions:**
- Not scalable, error-prone, no audit trails
- Zero automation for assessments or analytics
- Poor user experience for trainees and staff

### Urgency & Importance

**Why Now:**
1. **Upcoming cohort intake:** Next NSP cohort starts in Q1 2026—must have system operational
2. **Employment decision integrity:** Current manual process risks bias claims and lacks defensibility
3. **Trainer burnout:** Assessment creation burden is unsustainable—trainers requesting relief
4. **Competitive advantage:** Modern training infrastructure enhances company's reputation as top employer for graduates
5. **Data-driven culture:** Company increasingly requires metrics and KPIs—training center lacks this capability

---

## Proposed Solution

### Core Concept

TCMS is a **cloud-based, role-tailored platform** that:
1. **Manages content** migrated from Microsoft Loop with structured curriculum hierarchy (Program → Cohort → Specialization → Module → Topic)
2. **Generates assessments** using AI (Claude/GPT-4) from topic content, with configurable trainer oversight
3. **Tracks progress** at topic-level granularity, enabling self-paced learning while enforcing module deadlines
4. **Facilitates grading** with TA queue management, rubric-based lab reviews, and feedback delivery
5. **Powers employment decisions** through automated performance metrics, configurable thresholds, and three-level review workflows (Chapter Head → Program Head → Training Center Head)

### Key Differentiators

**vs. Generic LMS:**
- Built for **self-paced + deadlines** model (not rigid course schedules)
- AI assessment generation (not just question banks)
- Employment decision module (not just grade tracking)
- Flexible specialization management (easy to add 7th, 8th specialization)

**vs. Manual Processes:**
- 90% reduction in assessment creation time
- Real-time analytics (not weekly reports)
- Consistent rubrics and audit trails
- Trainee self-service progress visibility

**vs. Code Training Platforms:**
- Full program lifecycle (onboarding → learning → assessment → employment)
- Multi-role workflows (not just learner-focused)
- Cohort overlap support (NSP and GTP running concurrently)
- Company-specific content and evaluation criteria

### High-Level Vision

**Phase 1 (MVP - 6 months):** Core learning engine, AI assessment generation, basic analytics, employment decision framework

**Phase 2 (Months 7-12):** Advanced analytics, mobile app, discussion forums, automated code quality analysis for labs

**Phase 3 (Year 2+):** AI learning coach, predictive analytics for at-risk trainees, industry skills gap integration, dynamic curriculum optimization

---

## Target Users

### Primary User Segment: Trainees (GTP & NSP)

**Profile:**
- **Demographics:** Recent graduates (GTP) or national service personnel (NSP), ages 21-25, tech-focused education backgrounds
- **Scale:** ~100 NSP trainees + ~20-40 GTP trainees per year
- **Technical proficiency:** Comfortable with web applications; varying skill levels in their specialization (beginner to intermediate)

**Current Behaviors:**
- Self-study from Microsoft Loop documents
- Submit labs via email or shared drives
- Ask TAs for help via messaging apps (WhatsApp, Slack)
- Track own progress in personal notes/spreadsheets

**Specific Needs:**
- Clear curriculum roadmap ("What do I need to learn? In what order?")
- Real-time feedback on assessments (not weeks later)
- Visibility into own performance ("Am I on track? What's my score?")
- Deadline management ("What's due next? Am I behind?")
- Fair, consistent assessment (same standards for all trainees)

**Goals:**
- Complete training program on time
- Score well enough to secure employment offer
- Gain marketable technical skills
- Receive constructive feedback to improve

---

### Secondary User Segment: Training Staff (TAs, Trainers, Heads)

**Profile:**
- **TAs:** Junior developers or recent high-performers from previous cohorts; 2-5 TAs per specialization
- **Trainers:** Mid-level to senior developers; 1-3 trainers per specialization
- **Head of Chapter:** Senior technical lead; 1 per specialization (6 total)
- **Head of Program:** Senior manager; 1-2 (GTP/NSP may be same person)
- **Head of Training Center:** Director-level; 1 person

**Current Behaviors:**
- Trainers create content in Microsoft Loop, manually write questions in Word docs
- TAs receive lab submissions via email, grade in isolation, send feedback via email
- Heads request reports from trainers/TAs, analyze in Excel
- Employment decisions made in meetings with printed performance summaries

**Specific Needs:**
- **TAs:** Efficient grading queue, standardized rubrics, feedback templates, visibility into assigned trainees
- **Trainers:** Fast assessment creation, content editing tools, trainee performance insights per topic
- **Heads of Chapter:** Team management, curriculum quality analytics, question approval workflows
- **Heads of Program:** Cross-chapter performance visibility, at-risk trainee identification, employment readiness dashboards
- **Head of Training Center:** System-wide analytics, user management, evaluation criteria configuration, final employment decision authority

**Goals:**
- Reduce time spent on administrative tasks
- Provide high-quality, timely feedback to trainees
- Identify struggling trainees early for intervention
- Make fair, data-backed employment decisions
- Continuously improve curriculum based on performance data

---

## Goals & Success Metrics

### Business Objectives

- **Trainer time savings:** Reduce assessment creation time by 80% (from ~30 hours to ~6 hours per module) through AI generation
- **TA efficiency:** Reduce lab grading turnaround from 2-3 days to <24 hours through queue management and rubrics
- **Decision confidence:** 100% of employment decisions supported by documented performance data and audit trails
- **Scalability:** Support 150+ trainees per cohort (50% growth) without additional staff
- **Launch timeline:** MVP operational for Q1 2026 NSP cohort intake (6 months from kickoff)

### User Success Metrics

- **Trainee engagement:** 90%+ login rate weekly; average 10+ hours per week on platform
- **Assessment completion:** 95%+ of trainees complete all KCs and MAs within deadlines
- **Feedback timeliness:** 90%+ of labs graded within 24 hours
- **Trainee satisfaction:** 80%+ satisfaction score on post-program survey ("TCMS helped me learn effectively")
- **Staff adoption:** 100% of trainers and TAs actively using platform (zero reversion to manual processes)

### Key Performance Indicators (KPIs)

- **System uptime:** 99.5% availability during business hours (8am-8pm WAT)
- **AI question quality:** 85%+ trainer approval rate on AI-generated questions (in review mode)
- **Data integrity:** Zero grade calculation errors or data loss incidents
- **Performance insight:** Head of Training Center accesses analytics dashboard 3+ times per week
- **Employment outcomes:** 70%+ of trainees meeting performance thresholds receive employment offers (validate that system correctly identifies qualified candidates)

---

## MVP Scope

### Core Features (Must Have)

1. **User Authentication & Role Management**
   - Microsoft SSO integration (company email/account)
   - Six role types: Trainee, TA, Trainer, Head of Chapter, Head of Program, Head of Training Center
   - Role-based access control with scope assignments (e.g., Head of Backend can only manage Backend specialization)
   - User provisioning interface for Head of Training Center

2. **Content Management**
   - Bulk import from Microsoft Loop (one-time migration)
   - Curriculum hierarchy: Program → Cohort → Specialization → Module → Topic
   - Rich text editor for topic content creation/editing **by both Trainers AND TAs**
   - **Content editing scope:** Users can only edit content in their assigned specializations
   - **Immediate publishing:** No approval workflow - content goes live immediately when saved
   - Content asset upload (PDFs, videos, code samples, links)
   - Immediate content updates visible to all active trainees (no versioning gates)
   - **Version history:** Track content changes with rollback capability (safety mechanism)

3. **Self-Paced Learning Engine**
   - Trainees can browse and access all modules/topics in their specialization
   - Progress tracking at topic level (not started, in progress, completed)
   - Topic completion criteria: Pass both KC and MA
   - Module completion criteria: Complete all topics + submit lab
   - Jump-ahead capability (no forced sequencing)
   - Deadline enforcement per module (system tracks on-time vs late completion)

4. **AI-Powered Assessment Generation**
   - AI generates Knowledge Checks (30+ questions per topic, moderate-hard difficulty)
   - AI generates Module Assessments (30+ questions per topic, very hard difficulty)
   - Question types: Single-answer MCQ, multi-select MCQ, coding analysis MCQ
   - Question pool management (randomized subset presented to trainees)
   - Hybrid workflow: KCs auto-publish (Yolo mode), MAs require trainer review (Safe mode)
   - Trainer controls: View, edit, approve, regenerate questions
   - Question performance analytics (flag questions with <30% or >90% success rates)

5. **Assessment Taking & Scoring**
   - **Trainees attempt KCs with 3 attempts, MAs with 2 attempts** (configurable per assessment)
   - **No retaking after passing** - once trainee passes, score is final
   - Randomized question selection from pool (prevents memorization/cheating)
   - Auto-grading for MCQs
   - Immediate score feedback after attempt
   - Show correct answers after final attempt exhausted
   - Attempt history visible to trainee

6. **Lab Submission & Grading**
   - Lab assignment per module (description, requirements, rubric created by trainer)
   - **Primary submission method: GitHub repository link** (system validates link accessibility)
   - **Secondary submission method: File upload** (code files, documents, zip archives - fallback option)
   - **Repository snapshot:** System archives repo state at submission time (prevents post-submission changes)
   - **Repository visibility requirement:** Must be public repos
   - Final submission confirmation (no resubmissions allowed)
   - **TA-mentee grading model:** TAs assigned specific trainees based on specialization (mentor-mentee relationship); TAs grade only their assigned mentees' labs
   - Rubric-based grading interface
   - Text feedback field (required before grade submission)
   - Email notification to trainee when lab graded
   - Graded labs visible in trainee dashboard with score and feedback
   - **Future integration:** Prepares for Phase 2 AI Code Review Agent

7. **Trainee Dashboard**
   - Current specialization and cohort displayed
   - Progress visualization: completed topics/modules, percentage completion
   - Upcoming deadlines (sortable by urgency)
   - Recent scores (KCs, MAs, Labs) with averages
   - On-time submission status
   - Recommended next steps ("Complete Module 3 Lab by Oct 30")

8. **TA & Trainer Dashboards**
   - **TA:** **Assigned mentees list** (specialization-based), pending lab submissions from mentees, mentee progress summaries, content editing tools for assigned specialization
   - **Trainer:** Content management shortcuts, assessment question review queue, trainee performance in their specialization (average scores per topic), content editing tools for assigned specialization

9. **Head Dashboards (Chapter, Program, Training Center)**
   - **Head of Chapter:** Chapter-wide analytics (topic difficulty analysis, trainer/TA assignments, question approval queue)
   - **Head of Program:** Cohort performance overview (completion rates, average scores by specialization, at-risk trainees)
   - **Head of Training Center:** System-wide analytics (all cohorts, all specializations), user management, evaluation criteria configuration

10. **Performance Metrics & Employment Decision Support**
    - Auto-calculated trainee metrics: KC avg, MA avg, Lab avg, Overall technical score (weighted), Completion rate, On-time submission rate, Improvement trend
    - Monthly performance snapshots (stored for audit trail)
    - **Configurable evaluation thresholds per cohort + specialization** (min KC %, min MA %, min Lab %, min completion %, min on-time %)
    - **Threshold configuration permissions:** Only Heads of Program and Head of Training Center can modify thresholds
    - Red flag alerts (trainees below thresholds)
    - Three-level review workflow: Head of Chapter adds notes → Head of Program makes recommendation → Head of Training Center makes final decision
    - Soft skills score input (manual entry, tracked separately)
    - Employment decision export report (PDF/Excel)

11. **Notifications & Communication**
    - Email notifications for: Upcoming deadlines (3 days, 1 day before), missed deadlines, lab graded, new announcements
    - In-platform announcements (Program-wide, Cohort-wide, Specialization-wide)
    - Notification preferences (trainees can toggle email notifications)

12. **Admin & System Management**
    - Create new programs, cohorts, **specializations (can be added mid-year but won't be assigned unless needed)**, modules, topics
    - Enroll trainees into cohort + specialization
    - Assign trainers and TAs to specializations and cohorts  (TA-mentee ratio TBD)
    - **TA assignment model:** Assign specific trainees to TAs based on specialization for mentorship
    - Set deadlines per module per cohort
    - Configure assessment attempt limits (KC: 3, MA: 2, Lab: 1)
    - Configure evaluation criteria and thresholds (Heads of Program and Training Center only)
    - Audit logs (user actions, grade changes, employment decisions, content changes)

---

### Out of Scope for MVP

- Mobile native apps (iOS/Android) - web-responsive only for MVP
- Discussion forums or Q&A features
- Real-time chat/messaging between users
- Video conferencing integration
- Automated code quality analysis (static analysis, linting) for labs
- Predictive analytics (at-risk prediction models)
- Gamification (badges, leaderboards, achievements)
- Peer review or collaboration features
- Content versioning with trainee-specific views
- Multi-language support (English only for MVP)
- Capstone project management (if exists, treated as final module lab)
- Integration with external learning platforms (LeetCode, Coursera)
- Advanced reporting (custom report builder, scheduled reports)
- API for third-party integrations

---

### MVP Success Criteria

**MVP is successful if:**
1. One full cohort (NSP or GTP) completes entire training cycle using TCMS (onboarding → learning → assessment → labs → employment decision)
2. 90%+ of trainers and TAs prefer TCMS over manual processes (measured via survey)
3. Zero grade calculation errors or data loss incidents during pilot cohort
4. AI-generated assessments achieve 80%+ trainer approval rate (quality validation)
5. Head of Training Center successfully uses performance dashboards to make employment decisions with documented audit trail
6. Lab grading turnaround averages <48 hours (improvement from 2-3 days)
7. System handles 100+ concurrent trainees without performance degradation (<3 second page loads)

---

## Post-MVP Vision

### Phase 2 Features (Months 7-12)

**🔥 HIGH PRIORITY: AI Code Review Agent**
- **Automated GitHub lab review:** When trainee submits GitHub link, AI agent automatically analyzes code against lab requirements
- **Intelligent feedback:** AI provides detailed review on code quality, best practices, potential bugs, adherence to requirements
- **Preliminary grading:** AI suggests grade based on analysis
- **TA workflow integration:** TA reviews AI feedback and makes final decision (AI assists, human approves)
- **Benefits:** Instant feedback for trainees, 70%+ reduction in TA grading time, scales to unlimited submissions
- **Timeline:** 6-9 months post-MVP (high ROI)

**Enhanced Collaboration:**
- Discussion forums per topic for trainee Q&A
- TA office hours scheduling system
- Peer code review workflows for labs

**Advanced Analytics:**
- Curriculum difficulty heatmaps (which topics are hardest across cohorts?)
- Trainer effectiveness metrics (trainee success rates by trainer)
- Custom report builder for Heads
- Data export (CSV, Excel) for external analysis

**Mobile Experience:**
- React Native mobile app for iOS/Android
- Offline content viewing
- Push notifications for deadlines and feedback

**Content Enhancements:**
- Interactive code playgrounds in lessons
- Video embedding and transcripts
- Quizzes within lesson content (formative, not graded)

### Long-term Vision (Year 2+)

**AI Learning Coach:**
- Conversational AI assistant answering trainee questions about content
- Personalized study recommendations based on performance
- Automated encouragement and intervention messages

**Predictive Analytics:**
- Employment likelihood predictions (early warning system)
- Recommended intervention strategies for at-risk trainees
- Topic difficulty predictions for new content

**Dynamic Curriculum:**
- A/B testing of different content/assessment approaches
- Automated curriculum optimization recommendations based on cohort performance

**Industry Integration:**
- Skills gap analysis (company hiring needs vs. trainee competencies)
- Real-time job market data influencing curriculum priorities
- External certification preparation (AWS, Azure, Google Cloud)

### Expansion Opportunities

**Internal Expansion:**
- Onboarding training for all new hires (beyond GTP/NSP)
- Continuing education for existing employees (upskilling programs)
- Soft skills and leadership training modules

**External/Commercial:**
- White-label TCMS for other companies with training programs
- SaaS offering for corporate training centers
- Partner with universities for student training programs

**Geographic:**
- Multi-region deployment for international offices
- Localization (French, Portuguese for West African market)

---

## Technical Considerations

### Platform Requirements

- **Target Platforms:** Web application (desktop and mobile-responsive); mobile apps in Phase 2
- **Browser Support:** Chrome, Firefox, Safari, Edge (latest 2 versions); IE not supported
- **Performance Requirements:**
  - Page load: <3 seconds on 4G connection
  - Assessment submission: <1 second response time
  - Support 100+ concurrent users without degradation
  - File upload: Support up to 50MB lab submissions
- **Accessibility:** WCAG 2.1 AA compliance (keyboard navigation, screen reader support)

### Technology Preferences

**Frontend:**
- **Framework:** React (with TypeScript) - team familiarity, component ecosystem, mobile (React Native) path
- **State Management:** Redux Toolkit or Zustand - predictable state for complex workflows
- **UI Library:** Material-UI (MUI) or Chakra UI - rapid development, accessible components
- **Rich Text Editor:** Quill or TipTap - for content authoring

**Backend:**
- **Framework:** Node.js (Express) or Python (FastAPI) - team preference and AI integration ease
- **API Style:** RESTful for CRUD, consider GraphQL for complex dashboard queries
- **Authentication:** Microsoft OAuth 2.0 / Azure AD integration
- **Background Jobs:** Bull (Node.js) or Celery (Python) - for AI question generation, notification sending

**Database:**
- **Primary:** PostgreSQL - relational data (users, content, assessments), JSONB for flexibility
- **Caching:** Redis - session management, performance metrics aggregation, queue management
- **File Storage:** Azure Blob Storage - lab submissions, content assets (videos, PDFs)

**AI/ML:**
- **LLM Provider:** OpenAI GPT-4 or Anthropic Claude (via API) - question generation from content
- **Backup Option:** Azure OpenAI Service - enterprise compliance, data residency

**Hosting/Infrastructure:**
- **Cloud Provider:** Microsoft Azure (preferred) - company Microsoft ecosystem, SSO integration, regional presence
- **Compute:** Azure App Service or AKS (Kubernetes) if containerized
- **CI/CD:** GitHub Actions or Azure DevOps Pipelines
- **Monitoring:** Azure Application Insights + Sentry for error tracking
- **Email:** Microsoft 365 SMTP or SendGrid

### Architecture Considerations

**Repository Structure:**
- Monorepo (recommended): Shared types between frontend/backend, atomic commits, unified versioning
- Alternative: Separate repos for frontend, backend, shared types package

**Service Architecture:**
- Monolith for MVP (faster development, simpler deployment)
- Prepare for microservices (Phase 2): AI service, notification service, analytics service could be split

**Integration Requirements:**
- Microsoft SSO (OAuth 2.0 / Azure AD) - MUST HAVE for MVP
- Microsoft Loop export - one-time bulk import script (can be manual process with guidance)
- Email service (Microsoft 365 or SendGrid) - MUST HAVE for notifications
- AI API (OpenAI/Anthropic) - MUST HAVE for assessment generation

**Security/Compliance:**
- **Authentication:** Microsoft SSO only (no password management)
- **Authorization:** Role-based access control (RBAC) with fine-grained permissions
- **Data Encryption:** TLS 1.3 in transit, AES-256 at rest
- **Audit Logging:** All grade changes, employment decisions, admin actions logged with timestamp and user ID
- **Data Privacy:** Trainee performance data visible only to authorized roles; no cross-cohort data leakage
- **Backup & Recovery:** Daily automated backups, 30-day retention, <4 hour recovery time objective (RTO)
- **GDPR/Local Compliance:** May need data residency in-country (Nigeria?) - verify legal requirements

---

## Constraints & Assumptions

### Constraints

**Budget:**
- Development budget: TBD (estimate $150K-250K for 6-month MVP with 3-4 developers)
- Infrastructure budget: ~$500-1000/month (Azure hosting + AI API calls at 100 trainees scale)
- Ongoing: ~$1500-2500/month operational costs (hosting, APIs, maintenance)

**Timeline:**
- MVP launch: 6 months (hard deadline for Q1 2026 cohort intake)
- Pilot cohort: 6-12 months (observe full training cycle)
- Iterative improvements: Ongoing post-launch

**Resources:**
- Development team: 1 backend, 1 frontend, 1 full-stack, 1 QA (estimated)
- Design: Outsourced or part-time UX designer
- Product management: BMAD team member as product owner
- Subject matter experts: Training staff available for requirements clarification and UAT

**Technical:**
- Must integrate with Microsoft ecosystem (SSO, email)
- No custom mobile apps until Phase 2 (web-responsive only)
- AI API rate limits and costs constrain question generation frequency
- Must support offline content migration from Microsoft Loop (no real-time sync)

### Key Assumptions

- Company has Azure subscription or willingness to establish one
- Training staff will dedicate time for UAT and feedback during development
- Trainees have reliable internet access (4G minimum) and modern devices
- Content in Microsoft Loop is well-structured and export-friendly
- GTP program is 6 months (pending confirmation)
- AI-generated questions will achieve 80%+ quality threshold with prompt engineering
- 100 trainees is the target scale for MVP (not 500+)
- Employment decisions incorporate soft skills data from separate process (out of scope)
- English is the primary language (no localization needed for MVP)
- Labs are submitted as files (not live code execution environments)

---

## Risks & Open Questions

### Key Risks

- **AI Question Quality Risk:** AI-generated assessments may not meet difficulty or accuracy standards, requiring extensive trainer rework
  - *Impact:* High (defeats purpose of AI generation)
  - *Mitigation:* Pilot AI generation with 2-3 topics, iterate prompts, implement review workflow, maintain option for manual question creation

- **Change Adoption Risk:** Training staff resist new system, revert to manual processes
  - *Impact:* High (MVP failure)
  - *Mitigation:* Involve trainers/TAs in design process, provide training, launch with pilot cohort (not all cohorts at once), gather feedback iteratively

- **Data Migration Risk:** Content from Microsoft Loop doesn't map cleanly to TCMS structure, requiring manual cleanup
  - *Impact:* Medium (delays launch)
  - *Mitigation:* Analyze Loop content structure early, develop migration scripts, allocate 2-3 weeks for cleanup, consider manual entry for small content volumes

- **Performance Risk:** System slow or unresponsive with 100+ concurrent users during assessment periods
  - *Impact:* High (unusable during peak times)
  - *Mitigation:* Load testing before launch, database indexing, caching strategy, auto-scaling on Azure, queue assessments if needed

- **Scope Creep Risk:** Training staff request features beyond MVP, delaying launch
  - *Impact:* Medium (missed Q1 2026 deadline)
  - *Mitigation:* Strict MVP scope definition, feature backlog for Phase 2, product owner enforces prioritization

- **Fairness/Bias Risk:** Employment decisions perceived as unfair due to inconsistent assessments or grading
  - *Impact:* High (legal/reputational risk)
  - *Mitigation:* Standardized rubrics, question performance analytics, audit trails, trainer oversight on AI-generated content, pilot cohort review before full rollout

### Open Questions

**Program Structure:**
1. ⏳ Confirm GTP program duration (6 months assumed)
2. ⏳ Are there capstone projects, and if so, how do they differ from labs?
3. ✅ **ANSWERED:** Specializations can be added mid-year but won't be assigned unless needed

**Assessment Rules:**
4. ✅ **ANSWERED:** KC attempts = 3, MA attempts = 2, Lab attempts = 1 (FINAL)
5. ⏳ Time limits on assessments, or unlimited time?
6. ✅ **ANSWERED:** NO retaking after passing - score is final
7. ⏳ **NEW:** Do deadlines apply to KCs and MAs, or only to modules/labs? (Self-paced model clarification needed)

**Lab Workflows:**
8. ✅ **ANSWERED:** GitHub links (primary) + file uploads (secondary); repos must be public; system validates and snapshots
9. ✅ **ANSWERED:** TAs assigned specific mentees based on specialization (mentor-mentee relationship); TA-mentee ratio TBD
10. ⏳ If a lab submission is corrupted or incomplete, can trainee resubmit before grading starts? (Conflicts with "FINAL" rule)

**Content Management:**
11. ✅ **ANSWERED:** Both Trainers AND TAs can update content in their assigned specializations
12. ⏳ How often is content updated? (Weekly? Per cohort? Annually? As needed?)
13. ✅ **ANSWERED:** No approval workflow - immediate publishing; version history for rollback

**Employment Decisions:**
14. ⏳ What are the actual threshold values? (e.g., 70% KC average, 75% MA average?) - **To be configured per cohort**
15. ⏳ How is the overall technical score weighted? (KC 20%, MA 40%, Lab 40%?) - **Configurable**
16. ✅ **ANSWERED:** Yes, thresholds can vary by specialization (configurable per cohort + specialization)
17. ⏳ Is there an appeals process if a trainee contests the employment decision?

**Soft Skills:**
18. ⏳ How/when are soft skills assessed? (Separate system? Manual forms?)
19. ⏳ Who inputs soft skills scores into TCMS? (TAs? Trainers? HR?)

**Technical:**
20. ⏳ Are there existing company policies on data residency, encryption, or compliance we must follow?
21. ⏳ Is there a company-standard tech stack we should use, or is team free to choose?
22. ⏳ What is the process for deploying to production? (DevOps team handles? Self-managed?)

**Additional Questions:**
23. ⏳ If a TA is unavailable, who grades their mentees' labs? (Backup TA? Trainer?)
24. ⏳ Can trainees see which TA is assigned as their mentor?

### Areas Needing Further Research

**User Research:**
- Interview 5-10 trainees from previous cohorts (pain points, desired features, workflow preferences)
- Shadow TAs during lab grading to understand actual workflow (vs. described workflow)
- Workshop with Heads to validate analytics dashboard mockups

**Technical Research:**
- Prototype AI question generation with 2-3 sample topics from different specializations (validate quality, cost, speed)
- Analyze Microsoft Loop content structure (schema mapping, export format, cleanup requirements)
- Load testing plan (tools, metrics, success criteria)

**Competitive Research:**
- Evaluate 3-5 enterprise LMS platforms (even if not purchasing, learn UI/UX patterns)
- Research other corporate training programs' tech stacks (what works? what doesn't?)

**Compliance Research:**
- Verify data privacy laws in Nigeria/West Africa (GDPR equivalent? Data residency requirements?)
- Consult company legal team on employment decision data retention and audit requirements

---

## Appendices

### A. Research Summary

**Brainstorming Session (October 23, 2025):**
- 4 focused brainstorming sessions conducted: System Architecture, User Workflows, AI Strategy, Employment Decisions
- 40+ architectural decisions documented
- Key insight: Flexibility is paramount—system must adapt to changing organizational needs
- Key insight: Self-paced + deadlines balance requires careful UX design (trainees need autonomy but also structure)
- Documented in: `docs/brainstorming-session-results.md`

**Initial Requirements Document:**
- Detailed prep document provided by BMAD team outlining current state, user personas, assessment types, AI requirements
- Identified 30+ open questions through systematic gap analysis
- Clarified critical distinctions: Module Assessments are per-topic (not per-module), very hard difficulty

**Technology Landscape:**
- Microsoft ecosystem already in use (Loop, Microsoft 365, likely Azure)
- Team familiar with modern web frameworks (React assumed based on industry trends)
- AI APIs (OpenAI, Anthropic) proven for educational content generation

### B. Stakeholder Input

**Training Staff Feedback:**
- "Be flexible—decisions change within organizations" → System must not hard-code organizational structure or rules
- "You should know" → Analyst expected to make reasonable design decisions without constant approval
- Labs are final submission (no resubmissions) → High-stakes UX must be foolproof
- Trainees can jump ahead → Progress tracking must support non-linear paths

**Leadership Priorities:**
- Head of Training Center is ultimate admin and decision authority
- Employment decisions directly impact company talent pipeline—data integrity is non-negotiable
- Scale to 100+ trainees without additional staff is critical business goal

### C. References

**Related Documents:**
- `docs/brainstorming-session-results.md` - Detailed brainstorming outcomes
- Initial requirements document (provided by BMAD team) - stored in project context

**Technology References:**
- Microsoft Azure Documentation: https://docs.microsoft.com/azure
- Microsoft Authentication Library: https://docs.microsoft.com/azure/active-directory/develop
- OpenAI API Documentation: https://platform.openai.com/docs
- Anthropic Claude API: https://docs.anthropic.com

**Similar Systems (for research):**
- Canvas LMS: https://www.instructure.com/canvas
- Coursera for Business: https://www.coursera.org/business
- LinkedIn Learning: https://learning.linkedin.com

---

## Next Steps

### Immediate Actions

1. **Validate GTP duration and attempt limits** - Confirm assumptions with training staff (1 day)
2. **Prototype AI question generation** - Test with 2-3 sample topics, evaluate quality and cost (1 week)
3. **Assemble development team** - Hire or assign developers, designer, QA (2 weeks)
4. **Kickoff workshop** - Review project brief with full team, align on priorities (1 day)
5. **Create wireframes for key screens** - Trainee dashboard, TA grading queue, Head analytics (2 weeks)
6. **Finalize tech stack** - Confirm Azure, database, frontend/backend frameworks (1 week)
7. **Set up development environment** - Repos, CI/CD, Azure subscriptions, dev databases (1 week)
8. **Begin PRD development** - Expand this brief into detailed Product Requirements Document with user stories (ongoing)

### PM Handoff

This Project Brief provides comprehensive context for the Training Center Management System. The next phase is to **create a detailed Product Requirements Document (PRD)** that translates this strategic vision into actionable development tasks.

**Recommended PRD sections:**
1. **User Stories & Acceptance Criteria** - Detailed "As a [role], I want [feature] so that [benefit]" for all 12 MVP features
2. **Wireframes & Mockups** - Visual designs for all key screens (dashboards, assessment taking, grading, admin)
3. **API Specifications** - Endpoint definitions, request/response formats, authentication flows
4. **Database Schema** - Detailed ERD with all tables, columns, relationships, indexes
5. **AI Integration Specifications** - Prompt templates, API call flows, quality validation logic
6. **Testing Strategy** - Unit, integration, load testing plans; UAT process with training staff
7. **Launch Plan** - Pilot cohort selection, rollout phases, success criteria, rollback plan
8. **Training & Documentation** - User guides per role, admin documentation, trainer onboarding

**Success Criteria for PRD:**
- Development team can start coding without ambiguity
- UX designer has clear requirements for all screens
- QA can write test cases from acceptance criteria
- Product owner can prioritize features and make trade-offs

---

*Prepared using the BMAD-METHOD™ Project Brief Framework*
