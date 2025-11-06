# Brainstorming Session Results

**Session Date:** 2025-10-23
**Facilitator:** Business Analyst Mary
**Participant:** BMAD Team

---

## Executive Summary

**Topic:** Training Center Management System - Core Architecture & Requirements

**Session Goals:**
- Fill knowledge gaps from initial requirements document
- Define comprehensive system architecture
- Establish user workflows for 6 personas
- Design AI assessment generation strategy
- Create employment decision framework
- Build solid foundation for PRD development

**Techniques Used:**
- Structured Gap Analysis
- Systematic Requirements Elicitation
- User Journey Mapping
- Technical Architecture Design
- Decision Framework Modeling

**Total Ideas Generated:** 40+ architectural decisions, workflows, and system features

### Key Themes Identified:
- Flexibility is paramount - system must adapt to changing organizational needs
- Self-paced learning with deadline accountability
- AI-powered assessment generation with configurable oversight
- Data-driven employment decisions with human judgment layer
- Clear role-based access and responsibilities
- Content migration from Microsoft Loop to platform

---

## Technique Sessions

### Session 1: Gap Analysis & Requirements Clarification - 45 minutes

**Description:** Systematic review of initial requirements document to identify missing information, validate assumptions, and clarify ambiguities

#### Ideas Generated:
1. Program structure: NSP (12 months) and GTP (6 months) start at different times but can overlap
2. Self-paced learning model with flexible deadlines (verification needed on whether deadlines apply to KCs/MAs/Labs)
3. Trainees know their specialization track upfront (no exploratory phase)
4. **Assessment attempts confirmed:** KCs (3 attempts), MAs (2 attempts), Labs (1 attempt - FINAL)
5. Lab submissions are final - no resubmissions allowed; no retaking after passing any assessment
6. Content updates are immediately visible to all active trainees
7. Scale: ~100 NSP trainees, fewer GTP trainees per cohort
8. Assessment structure clarified: KCs and MAs are BOTH per-topic (not module-level)
9. Module Assessments are 30 very difficult questions per topic
10. **Labs are submitted via GitHub links (primary) or file uploads (secondary)**
11. **TA-mentee model:** TAs assigned specific trainees based on specialization (mentor-mentee relationship)
12. **Content publishing:** Both Trainers AND TAs can edit and publish content in their assigned specializations immediately
13. **Specialization flexibility:** New specializations can be added mid-year but won't be assigned unless needed

#### Insights Discovered:
- Initial assumption about Module Assessments being per-module was incorrect - they're per-topic with higher difficulty than KCs
- The organization values flexibility over rigid processes - "decisions change within organizations"
- Employment decisions involve both technical and soft skills data, with heads setting thresholds
- Microsoft SSO integration simplifies authentication
- Focus should remain on 6 core user personas rather than expanding to HR/admin roles initially

#### Notable Connections:
- Self-paced + deadlines = system must track both progress AND time-based compliance
- Final lab submissions + employment stakes = need for clear submission confirmation UX
- Content updates go live immediately = versioning is informational only, not gating
- Flexible specializations = database schema must be easily extensible

---

### Session 2: System Architecture & Data Model Design - 30 minutes

**Description:** Design of comprehensive data model supporting flexible, multi-cohort, self-paced training programs

#### Ideas Generated:
1. Hierarchical content structure: Program → Cohort → Specialization → Module → Topic → Assessments
2. Separate tables for KCs, Module Assessments, and Labs with distinct rules
3. Question pool management with 30+ questions per topic per assessment type
4. Trainee progress tracking at topic level (not just module completion)
5. Role-based access control with scope assignments (e.g., Head of Backend = scope: backend_specialization)
6. Performance metrics table with snapshot capability for audit trail
7. Configurable evaluation criteria per cohort + specialization
8. Content asset management for migrated Microsoft Loop materials
9. Multi-tenant data isolation despite overlapping cohorts
10. Question metadata tracking (difficulty, usage stats, performance analytics)

#### Insights Discovered:
- Topic-level progress tracking enables true self-paced learning (jump ahead capability)
- Snapshot approach for performance metrics supports historical analysis and appeals
- Separating evaluation criteria from actual performance data enables flexible threshold adjustments
- Question performance analytics (success rates) can flag problematic questions automatically

#### Notable Connections:
- Self-paced progression requires calculated "next available" logic per trainee
- Employment decisions need both current snapshot and historical trend data
- AI question pools need minimum size (30+) but recommend 50+ for randomization
- Content versioning connects to audit trail for fairness in evaluation

---

### Session 3: User Workflows & Key Features - 25 minutes

**Description:** Mapped end-to-end workflows for all 6 user personas from onboarding through employment decisions

#### Ideas Generated:
1. **Trainee workflow:** Onboarding → Self-paced learning → Assessment attempts (KC: 3, MA: 2) → Lab submission via GitHub/files (FINAL) → Progress tracking → Feedback receipt
2. **TA workflow:** View assigned mentees → Grade mentees' labs (specialization-based assignment) → Rubric-based review → Feedback delivery → Mentee monitoring → At-risk identification
3. **Trainer workflow:** Content management (edit & publish in assigned specialization) → Assessment configuration → AI question review/approval → Optional mentoring
4. **Head of Chapter workflow:** Curriculum ownership → Trainer/TA assignment to specialization → Quality assurance → Performance analysis
5. **Head of Program workflow:** Cohort creation → Cross-chapter monitoring → Configure evaluation thresholds → Employment readiness assessment
6. **Head of Training Center workflow:** Strategic oversight → System-wide analytics → Configure evaluation thresholds → Final employment authority
7. Email notifications for deadlines and feedback availability
8. Dashboard for trainees showing completion, scores, deadlines, on-time status
9. Analytics dashboards per role showing relevant performance data
10. Deadline alert system with escalation (approaching, missed)
11. **GitHub link validation:** System validates link accessibility before accepting submission
12. **Repo snapshot:** System archives repo state at submission time (prevents post-submission changes)

#### Insights Discovered:
- Each role has distinct dashboard needs - not one-size-fits-all
- **TAs manage specific mentees (not a shared queue)** - relationship-based grading within their specialization
- Trainers need bulk operations for question approval (not one-by-one review)
- Employment decision workflow involves 3 levels of review (Chapter → Program → Training Center)
- Trainee transparency is important but selective (see scores, not employment predictions)
- **GitHub-first submission model** requires link validation and repo snapshot capability
- **Content governance simplified:** Both Trainers and TAs can publish immediately in their specializations

#### Notable Connections:
- TA grading workflow connects to trainee notification system
- Head dashboards need drill-down capability (cohort → specialization → trainee)
- Self-paced model requires "recommended next steps" guidance for trainees
- At-risk identification should trigger proactive TA/trainer intervention

---

### Session 4: AI Assessment Generation Strategy - 20 minutes

**Description:** Designed AI-powered question generation system with flexible oversight models

#### Ideas Generated:
1. **Input to AI:** Topic content + learning objectives + difficulty target + question count + question types
2. **AI Process:** Content analysis → Question generation → Quality checks → Output to question pool
3. **Three workflow modes:** Auto-publish (Yolo), Review-before-publish (Safe), Hybrid (recommended)
4. **Hybrid approach:** Auto-publish KCs (lower stakes), review MAs (higher stakes), manual Labs
5. **Trainer controls:** Toggle auto-publish per specialization/module, bulk approve, edit, regenerate
6. **Question pool size:** Minimum 30, recommend 50+ per topic per assessment type
7. **Randomization:** Trainees receive randomized subset from pool (prevent cheating)
8. **Question analytics:** Track success rates, flag questions with <30% or >90% success
9. **Quality checks:** Grammar validation, answer verification, duplicate detection, difficulty calibration
10. **Question lifecycle:** Draft → Under Review → Active → Archived

#### Insights Discovered:
- Flexibility in AI oversight allows organizations to find their comfort level
- Question performance analytics can continuously improve assessment quality
- Larger question pools increase security and reduce memorization risk
- Auto-flagging problematic questions reduces trainer burden

#### Notable Connections:
- AI workflow mode can be different per chapter (Backend auto-publish, Frontend review-required)
- Question analytics feed back into AI training for better generation
- Bulk approval workflow essential for scalability (thousands of questions across curriculum)
- Regeneration capability allows iterative improvement without starting from scratch

---

### Session 5: Employment Decision Framework - 25 minutes

**Description:** Designed comprehensive, configurable framework for data-driven employment decisions with human oversight

#### Ideas Generated:
1. **Auto-calculated metrics:** KC average, MA average, Lab average, Overall technical score (weighted), Completion rate, On-time submission rate, Improvement trend, Time to completion
2. **Configurable thresholds:** Set per cohort + specialization for all metrics
3. **Red flag alerts:** Auto-alert for <50% completion with 1 month remaining, <60% overall score in final month, <70% on-time rate
4. **Three-level review:** Head of Chapter → Head of Program → Head of Training Center
5. **Soft skills integration:** Manual input field, tracked separately but viewable in same dashboard
6. **Monthly snapshots:** Automated calculation and storage for historical tracking
7. **Employment readiness score:** Calculated metric (not visible to trainees)
8. **Audit trail:** All decisions logged with timestamp, decision-maker, and notes
9. **Trainee transparency:** See all scores and completion status, NOT employment predictions or peer comparisons
10. **Decision export:** Generate reports for final communication/HR handoff

#### Insights Discovered:
- Snapshot approach enables "what if" scenario analysis (e.g., change thresholds, recalculate)
- Improvement trend is as important as absolute scores (shows learning ability)
- Three-level review balances efficiency with thoroughness
- Soft skills as separate input respects that it's assessed through different process

#### Notable Connections:
- Performance snapshots connect to content versioning (fairness if curriculum changes)
- Red flag system enables early intervention rather than end-of-program surprises
- Configurable thresholds allow different standards per specialization (Backend vs UI/UX)
- Audit trail protects against bias/favoritism claims

---

## Idea Categorization

### Immediate Opportunities
*Ideas ready to implement in MVP*

1. **Self-Paced Topic Progression System**
   - Description: Trainees can jump ahead to any module but must complete all by deadline; system tracks topic-level completion
   - Why immediate: Core to the learning model, foundational feature
   - Resources needed: Topic progress table, completion calculation logic, UI for progress visualization

2. **AI Question Generation with Hybrid Oversight**
   - Description: AI generates KCs and MAs from topic content; KCs auto-publish, MAs require review
   - Why immediate: Critical for scaling assessment creation; reduces trainer burden significantly
   - Resources needed: AI API integration (OpenAI/Claude), question pool database, review workflow UI

3. **Role-Based Dashboards (6 Personas)**
   - Description: Each user role gets tailored dashboard showing relevant data (trainee: scores/deadlines; TA: grading queue; Heads: analytics)
   - Why immediate: Core UX requirement; users can't function effectively without role-appropriate views
   - Resources needed: Dashboard components per role, data aggregation queries, filtering logic

4. **Lab Submission with Final-Status Logic (GitHub + File Upload)**
   - Description: Trainees submit labs via GitHub link (primary) or file upload (secondary); link validation + repo snapshot at submission; FINAL submission (no resubmissions); clear confirmation UX; TAs grade assigned mentees' labs with rubric and feedback
   - Why immediate: High-stakes feature (affects employment); must be crystal clear to prevent mistakes; GitHub model prepares for AI code review in Phase 2
   - Resources needed: GitHub API integration for validation and archiving, file upload system, submission confirmation flow, TA mentee management interface, rubric builder

5. **Performance Snapshot System for Employment Decisions**
   - Description: Monthly auto-calculation of all metrics; stored as snapshots; configurable thresholds; three-level review workflow
   - Why immediate: Core business requirement; determines employment outcomes
   - Resources needed: Metrics calculation engine, threshold configuration UI, review workflow, audit logging

6. **Deadline Management & Email Notifications**
   - Description: Deadlines set per module per cohort; email alerts (approaching, missed); visible in trainee dashboard
   - Why immediate: Accountability mechanism for self-paced model; prevents trainees from falling behind
   - Resources needed: Email service integration (Microsoft), deadline tracking table, notification scheduler

7. **Microsoft SSO Authentication**
   - Description: Company email/account login; role assignment post-authentication
   - Why immediate: Security requirement; leverages existing company infrastructure
   - Resources needed: Microsoft OAuth integration, user provisioning workflow

8. **Content Migration from Microsoft Loop**
   - Description: Bulk import of existing topic content; in-platform editing with rich text editor
   - Why immediate: Can't launch without content; trainers need to own content updates going forward
   - Resources needed: Loop export/import scripts, rich text editor component, content versioning

---

### Future Innovations
*Ideas requiring development/research*

1. **Adaptive AI Question Difficulty**
   - Description: AI adjusts question difficulty based on trainee performance history; personalized assessment experience
   - Development needed: ML model for difficulty prediction; trainee performance profiling; A/B testing framework
   - Timeline estimate: 6-9 months post-MVP

2. **Collaborative Learning Features**
   - Description: Discussion forums per topic; peer code review system; group project support
   - Development needed: Forum infrastructure; code diff viewing; group submission workflows
   - Timeline estimate: 3-6 months post-MVP

3. **Mobile App for Trainees**
   - Description: Native iOS/Android app for content consumption, progress tracking, notifications
   - Development needed: React Native/Flutter development; offline mode; push notifications
   - Timeline estimate: 9-12 months post-MVP

4. **AI Code Review Agent for GitHub Lab Submissions** ⭐ HIGH PRIORITY
   - Description: When GitHub link submitted, AI agent automatically accesses repo, analyzes code against lab requirements and expectations, provides detailed review and preliminary grade
   - Why high priority: Dramatically reduces TA grading burden; provides instant feedback; scales to unlimited trainees
   - Development needed: GitHub API integration; AI code review agent (Claude/GPT-4 Code Interpreter); lab requirements database; integration with TA grading workflow (AI review + TA final approval)
   - Timeline estimate: 6-9 months post-MVP

5. **Predictive Analytics for At-Risk Trainees**
   - Description: ML model predicting employment likelihood; early intervention recommendations
   - Development needed: Historical data collection (2+ cohorts); ML model training; intervention playbook
   - Timeline estimate: 12+ months post-MVP (need data first)

6. **Gamification & Engagement Features**
   - Description: Badges, leaderboards, achievement tracking, progress celebrations
   - Development needed: Gamification engine; achievement rule system; social comparison settings
   - Timeline estimate: 6-9 months post-MVP

---

### Moonshots
*Ambitious, transformative concepts*

1. **AI-Powered Personal Learning Coach**
   - Description: Conversational AI assistant per trainee; answers questions about content; recommends study paths; provides encouragement
   - Transformative potential: Scales personalized support beyond TA/trainer capacity; 24/7 availability; learns from interactions
   - Challenges to overcome: LLM hallucination prevention; cost of API calls at scale; ensuring answers align with curriculum

2. **Dynamic Curriculum Optimization**
   - Description: System analyzes trainee performance across cohorts; recommends curriculum adjustments (reorder topics, split modules, adjust difficulty)
   - Transformative potential: Continuously improving curriculum based on evidence; data-driven pedagogical decisions
   - Challenges to overcome: Statistical significance with small cohorts; balance between consistency and optimization; change management

3. **Industry Skills Gap Integration**
   - Description: Real-time integration with job market data (LinkedIn, Indeed, company hiring needs); curriculum automatically adjusts to prioritize in-demand skills
   - Transformative potential: Always-relevant training; graduates perfectly aligned with industry needs
   - Challenges to overcome: API integrations; curriculum flexibility; validation of skill trends; speed of curriculum changes

4. **Virtual Pair Programming & Live Collaboration**
   - Description: Real-time code collaboration between trainees and TAs; screen sharing; co-editing; integrated video chat
   - Transformative potential: Replicates in-person mentoring experience remotely; enables synchronous help sessions
   - Challenges to overcome: Infrastructure cost; bandwidth requirements; scheduling complexity; code environment sync

---

### Insights & Learnings
*Key realizations from the session*

- **Flexibility as a first-class requirement:** The phrase "be flexible, you should know" signals that over-engineering rigid rules will fail. System must accommodate changing organizational needs.
- **Self-paced ≠ Unstructured:** Deadlines provide accountability structure while allowing autonomy. This balance is critical for adult learners.
- **Two types of topic assessments is unusual but intentional:** KC (moderate-hard) + MA (very-hard) per topic enables both comprehension check and mastery verification.
- **Final lab submissions increase stakes:** No resubmission rule means submission UX must be foolproof (confirmation dialogs, save drafts, preview).
- **Employment decisions are data-informed, not data-determined:** System provides metrics; humans make final call. Capturing qualitative notes is as important as quantitative scores.
- **Scale matters for TAs:** ~100 trainees means TAs need efficient queue management and bulk operations.
- **AI oversight preference varies by risk tolerance:** Hybrid model (auto-publish KCs, review MAs) balances efficiency with quality control.
- **Content ownership must shift to platform:** Migration from Loop isn't just a data transfer - it's a workflow change for trainers.
- **Transparency builds trust, but selective transparency protects psychology:** Trainees see their scores (empowering) but not employment predictions (reduces anxiety/gaming).

---

## Action Planning

### Top 3 Priority Ideas

#### #1 Priority: Core Data Model & Architecture Implementation
- **Rationale:** Foundation for everything else; must be solid and extensible from day one
- **Next steps:**
  1. Finalize database schema (all tables from Session 2 brainstorming)
  2. Set up development environment with selected tech stack
  3. Implement user authentication (Microsoft SSO)
  4. Build basic CRUD operations for Programs, Cohorts, Specializations, Modules, Topics
- **Resources needed:** Backend developer(s), database administrator, cloud infrastructure (Azure recommended for Microsoft integration)
- **Timeline:** 3-4 weeks for MVP data layer

#### #2 Priority: Self-Paced Learning Engine & Trainee Dashboard
- **Rationale:** This IS the product for trainees; must be intuitive and motivating
- **Next steps:**
  1. Design trainee dashboard wireframes (progress, scores, deadlines, next steps)
  2. Implement topic progression logic (completion tracking, unlocking)
  3. Build KC and MA taking interface (randomized questions from pool)
  4. Create deadline visualization and notification system
- **Resources needed:** Frontend developer(s), UX designer, notification service
- **Timeline:** 4-5 weeks for trainee-facing MVP

#### #3 Priority: AI Assessment Generation MVP
- **Rationale:** Differentiator; solves major pain point; demonstrates innovation
- **Next steps:**
  1. Select AI provider (OpenAI GPT-4, Anthropic Claude, Azure OpenAI)
  2. Develop prompt engineering for question generation from topic content
  3. Implement question pool database with draft/active states
  4. Build trainer review interface for MA approval workflow
  5. Create auto-publish pipeline for KCs
- **Resources needed:** AI/ML engineer, API budget ($500-1000/month estimated), trainer feedback for prompt tuning
- **Timeline:** 3-4 weeks for functional AI pipeline

---

## Reflection & Follow-up

### What Worked Well
- Systematic gap-filling approach uncovered critical clarifications early
- User journey mapping revealed workflow requirements that weren't obvious from initial document
- Flexible design approach aligns with organization's stated preference
- Three-phase brainstorming (Architecture → Workflows → AI Strategy) built understanding progressively

### Areas for Further Exploration
- ✅ **ANSWERED - Attempt limits:** KCs (3 attempts), MAs (2 attempts), Labs (1 attempt - FINAL)
- ✅ **ANSWERED - Retaking after passing:** NO - once passed, score is final
- ✅ **ANSWERED - Lab submission types:** GitHub links (primary) + file uploads (secondary)
- ✅ **ANSWERED - Content publishing:** Both Trainers and TAs can edit and publish content in their assigned specializations immediately
- ✅ **ANSWERED - Threshold permissions:** Heads of Program and Head of Training Center can configure thresholds
- ⏳ **PENDING - Assessment deadlines:** Verify if deadlines apply to KCs, MAs, and Labs (self-paced model needs clarification)
- ⏳ **PENDING - Rubric standardization:** Should lab rubrics be standardized per specialization or trainer-defined?
- ⏳ **PENDING - Soft skills assessment process:** How/when are soft skills evaluated? Who conducts them?
- ⏳ **PENDING - Content update notification:** When content changes mid-cohort, do trainees get notified?
- ⏳ **PENDING - Dispute resolution:** What if trainee contests a grade or feels assessment was unfair?
- ⏳ **PENDING - GTP duration confirmation:** Verify 6 months for GTP program
- ⏳ **PENDING - Capstone projects:** Confirm existence and structure of final projects

### Recommended Follow-up Techniques
- **Technical spike:** Prototype AI question generation with sample topic content to validate feasibility and quality
- **Wireframing workshop:** Create visual mockups for key screens (trainee dashboard, TA grading queue, Head analytics)
- **User story mapping:** Write detailed user stories for top 3 priority features to feed into development
- **Risk assessment workshop:** Deep dive on security, data privacy, and fairness concerns given employment stakes

### Questions That Emerged
- ✅ **ANSWERED - TA assignment:** TAs assigned specific mentees based on specialization (mentor-mentee model); ratio TBD; assigned for entire program (with flexibility)
- ✅ **ANSWERED - GitHub repo requirements:** Must be public repos; system validates link accessibility; snapshot taken at submission time
- ⏳ **PENDING - TA visibility:** Can trainees see which TA graded their lab?
- ⏳ **PENDING - Incomplete program:** What happens if trainee doesn't complete by program end date? Extension? Immediate disqualification?
- ⏳ **PENDING - Privacy regulations:** Are there any privacy regulations (GDPR, local laws) governing storage of trainee performance data?
- ⏳ **PENDING - AI content ownership:** Who owns the AI-generated content? Any IP concerns?
- ⏳ **PENDING - Disaster recovery:** What's the disaster recovery plan if system goes down during assessment period?
- ⏳ **PENDING - Employment tie-breaker:** How are ties broken in employment decisions (e.g., 10 strong candidates, 8 positions)?
- ⏳ **PENDING - TA backup:** If a TA is unavailable, who grades their mentees' labs?

### Next Session Planning
- **Suggested topics:**
  1. PRD deep dive - translate brainstorming into detailed Product Requirements Document
  2. Technical architecture design - system architecture diagram, tech stack finalization, API design
  3. MVP feature prioritization - ruthlessly cut scope to 3-month launch target
- **Recommended timeframe:** Within 1-2 days to maintain momentum
- **Preparation needed:**
  - Compile any existing technical documentation or diagrams
  - Gather sample content from Microsoft Loop for AI prototyping
  - Confirm budget and timeline constraints for PRD scoping

---

*Session facilitated using the BMAD-METHOD™ brainstorming framework*
