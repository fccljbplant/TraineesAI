# ExaminerAI — Deep Audit Report

*Conducted August 2026, prior to the TraineesAI modernization.*

## Tech Stack Summary

- **Framework**: Next.js 16.1 (App Router, Turbopack disabled via `cross-env TURBOPACK=0`), React 19, TypeScript 5
- **Language / Runtime**: TypeScript; `bun` for installs, `vitest` for tests
- **Database**: SQLite (default dev), with a separate `prisma/schema.prod.prisma` for prod (Postgres). Prisma ORM 6.11
- **Auth**: Custom JWT + bcrypt (`jsonwebtoken`, `bcryptjs`) — not NextAuth (despite being a dep). Session via cookies.
- **AI Provider**: DeepSeek primary (`deepseek-v4-flash`), Z.ai GLM-4.6 fallback, then empty fallback. Uses `openai` SDK (OpenAI-compatible). Token cache layer. Per-user daily rate limiting + RPM/RPD global limits.
- **UI**: Tailwind 4 + shadcn/ui (Radix primitives), `lucide-react` icons, `recharts`, `framer-motion`, `react-markdown`, `@dnd-kit` (sortable), `react-hook-form` + `zod`
- **State**: React Query, `zustand`, React hooks
- **Hosting**: Vercel (crons for `/api/students/check-alerts` daily 9am + `/api/assistant/escalation/run` daily midnight)

## Data Model Overview (Prisma — 1002 lines, 30+ models)

### Core learning/training
- **Course** — central entity. Domain-agnostic (any subject). JSON blobs for journey, project template, AI prompts, test config, report card template, assessment config. Has weeks → days hierarchy.
- **CourseWeek** → **CourseDay** — curriculum outline (title, objective, whyItMatters, topicsCovered, activity, deliverable, resources)
- **CourseEnrollment** — junction (userId, courseId, role: "student"|"instructor")
- **User** — 8 roles (`pending`, `student`, `instructor`, `coordinator`, `counselor`, `guardian`, `institution_admin`, `platform_admin`) + 10+ project fields, security Q&A, currentWeek/currentDay, selfPacedEnabled
- **ProjectTask**, **ProjectWeek**, **ProjectReport**, **CurriculumProgress** — student capstone project tracking
- **Interaction** — every practice-question answer (pillar, score, feedback, gaps, cognitiveLoad, confidence, metacognitive, plagiarismScore)
- **WeeklyTest**, **DailyTest** + **DailyTestAnswer** — Socratic test sessions (also carry psychAnalysis, examinerObs, examinerComment, plagiarismScore)
- **Competency** — per-topic mastery score
- **ReportCard** — weekly grade; has workHabits + examinerObservations columns
- **AICache**, **AIUsageLog** — AI response caching + token accounting

### Behavioral/psychological monitoring (TO BE REMOVED)
- **PsychologyObs** — confidence, communication, learningCurve, engagement, cognitiveLoad, metacognitive, remarks (written on every evaluate call)
- **PsychEvidence** — 7 dimensions: calibration, explanatory_depth, gaming_pattern, attribution (mindset), cognitive_load, srl_phase, fluency
- **ConfidenceRating** — self-rated confidence vs actual score (Dunning-Kruger detection)
- **WellbeingState** — green/warning/red tier per student
- **CrisisFlag** — self_harm_risk, severe_distress, disclosure, academic_crisis, behavioral_concern
- **StudentHealthSummary** — daily rollup: moodScore, engagementScore, frustrationCount, avoidanceCount, enthusiasmCount
- **StudentAlert** — type (psychological/educational/mentorship/safeguarding), severity, metric
- **MentorshipTouchpoint** — GROW coaching log
- **SkillMastery** — per-topic mastery trend
- **ChatSession** — has behavioralSignals + psychAnalysis JSON columns
- **CaseReview** + **CaseReviewResponse** — anonymized student case discussions
- **GrowthReport** — strengths, growthAreas, dimensionSnapshot, behavioralNotes

### Communication / admin
- **Message** — instructor↔student in-app mail
- **Comment** — instructor feedback on any entity + marksOverride
- **InstructorRule** — instructor-defined condition→action rules
- **GroupTask** + **GroupTaskSubmission** + **PeerAssessment** — course assignments + peer review
- **Event** — course calendar
- **GuardianLink** — guardian↔student relationship
- **Certificate**, **AccessGrant**, **AuditLog**, **PasswordResetRequest**, **RoleNavConfig**, **Institution**, **Setting**

## Student Flow (day-to-day)

The student sidebar has 4 main tabs + 3 shared:

1. **Home** — current week/day, avg score, week progress bar, capstone project banner
2. **Study** — 4 sub-tabs: Daily Check-in, Practice (AI generates Socratic question), Daily Test (3 Qs), Weekly Test (10-question Socratic examiner)
3. **Project** — Gantt chart of AI-generated tasks, project settings, weekly project reports
4. **Progress** — full report card history, competency map, score trends

Plus shared: **Course** (outline), **AI Tutor** (chat with teacher persona), **Messages**, **Settings**.

**Day-to-day routine**: open app → popup reminds what's due → mark curriculum day complete → answer 1 practice question → log daily check-in → take daily test → work on project tasks → take weekly test on Fridays. All test answers → AI evaluates → writes Interaction + PsychologyObs + Competency + runs analysis-pipeline (writes PsychEvidence, recomputes WellbeingState).

## Instructor Flow

5 tabs:
1. **Today** — quick triage: alerts, students needing attention, recent activity, AI Assistant
2. **Students** — roster sorted by attentionScore. Click → StudentPortfolioPage (1353 lines — full single-student view)
3. **Mentorship** — GROW coaching workflow, voice touchpoint logger, case review, instructor rules
4. **Assignments** — GroupTask CRUD + submissions grading + peer-assessment review
5. **Insights** — batch analytics charts

## AI Integration

**Provider**: DeepSeek primary, Z.ai fallback. Both via `openai` SDK. Token cache (1h TTL). Per-user daily rate limits + global RPM(60)/RPD(10k). Every call logged to `AIUsageLog`.

**Routes**:
- `/api/ai/tutor` — student AI Tutor (no grading, short conversational replies)
- `/api/ai/evaluate` — grades practice answers. Hard floor 50%. 7 plagiarism heuristics. Writes Interaction + PsychologyObs + bumps Competency.
- `/api/ai/weekly-test`, `/api/ai/practice`, `/api/ai/daily-test` — Socratic examiner flows
- `/api/ai/instructor-tutor` — staff AI Assistant (writes ChatSession with behavioralSignals + psychAnalysis)

**Prompts** (`ai-prompts.ts`, 595 lines): `GLOBAL_AI_RULES` (includes "CRITICAL behavioral monitoring" rule), `SHARED_EXAMINER_RULES` (includes "PSYCHOLOGICAL ASSESSMENT" rule), `weeklyTestSystemPrompt`, `questionGenPrompt`, `evaluatePrompt`. Prompts explicitly instruct AI to assess confidence/overconfidence/engagement/give-up patterns.

## What's Working Well (KEEP)

- **Course-centric architecture** — clean domain-agnostic design
- **AI Tutor** — well-designed teacher persona, context injection, Roman-Urdu support
- **Socratic testing** — conceptual questions, 4 pillars, beginner-friendly grading
- **Plagiarism detection** — heuristic + AI combined
- **Project-based learning** — AI-generated tasks, Gantt, milestones, reports
- **Course Outline** — DB-driven, structured
- **DailyTaskReminder** — well-engineered popup
- **Self-paced learning** — `selfPacedEnabled` flag
- **Comments + marks override** — human-in-the-loop
- **In-app Messages** — replaces WhatsApp
- **AskMyInstructor FAB** — context-prefilled email
- **Certificate generation** + verify-token
- **Audit logging** + RBAC + IDOR protection
- **AI cost controls** — token cache, rate limits, quotas

## What's Dated or Broken (CHANGE)

- `next.config.ts`: `typescript.ignoreBuildErrors: true` + `reactStrictMode: false` — type errors silently ship
- 8 user roles but role identity is muddled (overlapping aliases)
- Counselor role entirely built around pastoral monitoring (736-line dashboard)
- PrincipalDashboard (600 lines) + AdminPrincipalTab (484 lines) — institutional pastoral health views
- InstructorBehaviorTab explicitly monitors teachers' AI Assistant usage
- InstructorLoadPanel shows instructor their own "wellbeing/load tier"
- Behavioral fields inside Interaction / WeeklyTest / ReportCard — baked into schema
- PsychologyObs model still being written to (dead table per cleanup route comment)
- Daily cron auto-sends messages based on psych signals
- Safeguarding filter on every teacher→student comment
- Mixed test counts: config says 15 questions, prompt says 10
- No NextAuth despite being a dep — custom JWT auth reinvented
- Prisma schemas (dev + prod) risk of drift

## File Inventory

- **API routes**: 118 route handlers under `src/app/api/`
- **Components**: 84 .tsx files, 21,922 total lines in `src/components/examiner/`
- **Lib files**: 34 .ts files in `src/lib/`
- **Module files**: 45 files across 16 dirs in `src/modules/`
- **Prisma schema**: 1002 lines, 30+ models

### Largest components (by line count)
| Component | Lines |
|---|---|
| StudentPortfolioPage.tsx | 1,353 |
| CoursePlanner.tsx | 1,015 |
| AdminDashboard.tsx | 771 |
| CounselorDashboard.tsx | 735 |
| AppShell.tsx | 722 |
| CheckInPanel.tsx | 689 |
| SystemPanel.tsx | 642 |
| PrincipalDashboard.tsx | 600 |
| DailyTaskReminder.tsx | 544 |

---

*This audit informed the [MODERNIZATION_PLAN.md](./MODERNIZATION_PLAN.md).*
