# TraineesAI Modernization — Master Plan

## Project context

TraineesAI is the modernized successor to ExaminerAI (https://github.com/fccljbplant/ExaminerAI). It's a Next.js 16 SaaS platform for training fresh engineering internees.

**The core model:** AI does the training (teaching, Socratic testing, project task generation). Instructors (busy engineers) only monitor progress and mentor struggling students via in-app messages.

**The goal of this modernization:** Remove the behavioral/psychological surveillance layer that accumulated in ExaminerAI, modernize the UX, and sharpen the AI-trains + human-mentors model.

---

## Non-negotiable principles

1. **AI trains. Humans mentor.** Never blur these roles.
2. **Instructors are collaborators**, not subjects to be monitored.
3. **Students are learners**, not psychological subjects.
4. Every feature must answer: *"Does this help a busy engineer mentor with minimum time?"*
5. **Never break production.** Each phase ships independently.

---

## Progress (updated August 2026)

### Phase 1: Strip the surveillance layer — ✅ COMPLETE & DEPLOYED

**Committed:** `82f3fd6` + `eebc655` (on GitHub `main`)
**Deployed:** `dpl_2ckUDzxcfnycAXiUDKAAfHzcBWtH` — production live at examiner-ai-tau.vercel.app

Removed ~2,368 lines of behavioral/psychological monitoring code:
- Deleted 11 Prisma models (PsychologyObs, PsychEvidence, WellbeingState, CrisisFlag, StudentAlert, StudentHealthSummary, ConfidenceRating, MentorshipTouchpoint, CaseReview, CaseReviewResponse, GrowthReport)
- Stripped psych fields from 6 models (Interaction, WeeklyTest, DailyTest, DailyTestAnswer, ReportCard, ChatSession)
- Deleted Counselor + Guardian roles entirely
- Deleted 35+ files (psych lib, API routes, components, dashboards)
- Rewrote AI prompts to remove all behavioral/psychological instructions
- Re-enabled strict TypeScript (`ignoreBuildErrors: false`, `reactStrictMode: true`)
- Removed Vercel crons (check-alerts, escalation/run)
- Renamed to "TraineesAI" in metadata

### Phase 2: Modern training engine core — ✅ COMPLETE & DEPLOYED

**Inspired by:** Code-level audit from Qwen AI (7 concrete issues identified with real code evidence)

Built 5 new files + 1 new Prisma model + 1 new API endpoint:

| File | Purpose | Lines |
|---|---|---|
| `src/lib/assessment/adaptive.ts` | 5-level adaptive difficulty engine (replaces static QUESTION_TYPES ladder) | 69 |
| `src/lib/learning-signal.ts` | Transparent 0-100 signal from academic facts only (replaces psych pipeline) | 123 |
| `src/lib/ai-json.ts` | JSON mode + zod validation + repair retry (replaces brittle [-] marker parsing) | 167 |
| `src/app/api/today/summary/route.ts` | Single endpoint feeding TodayView (parallel DB queries, priority-based nextAction) | 190 |
| `src/components/examiner/student/TodayView.tsx` | Modern trainee landing screen — "what do I do next?" | 251 |
| `src/app/api/daily-test/route.ts` | Modernized: adaptive difficulty, JSON mode, DrillCard creation, visible degraded mode | 604 |

**Prisma additions:**
- `DrillCard` model — spaced repetition for wrong answers (userId, topic, questionDigest, explanation, dueAt, attempts, lastScore, masteredAt)
- `DailyTest.difficultyState` field — JSON storing adaptive difficulty state

**What it does:**
- Difficulty escalates/softens based on scores + explicit confidence tap (sure/guessing)
- Wrong answers (<60) auto-create DrillCards due in 2 days
- AI failures show visible "examiner temporarily unavailable" instead of silent canned replies
- TodayView answers "what do I do next?" in one screen (next action + learning signal + drills + mentor message)
- Learning Signal computed transparently from scores (45%) + completion (30%) + activity (25%)

### Phase 3: Slide viewer + proactive AI tutor — ⏳ PLANNED

- Build SlideViewer component (on-the-fly slide generation from CourseDay fields)
- Build AIPanel component (proactive bubbles, slide awareness)
- Add CourseDay fields: videoUrl, codeExamples, webImages
- Extend AI course generation prompt

### Phase 4: Simplify instructor experience — ⏳ PLANNED

- Reduce instructor dashboard to 3 tabs: Today / Students / Messages
- Redesign StudentPortfolioPage (remove psych tabs, keep Academic + Project + Messages)
- Recompute attention score from academic signals only
- Clean up module structure (delete empty skeleton modules)

### Phase 5: Polish + ship — ⏳ PLANNED

- Consolidate Prisma schemas (dev + prod identical except provider)
- Rename "ExaminerAI" → "TraineesAI" across all branding
- Final verification: lint 0 errors, tsc 0 errors, build succeeds, tests pass

---

## Architecture: AI trains, humans mentor

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   AI Train   │────▶│  AI Assess   │────▶│ Human Mentor │
│              │     │              │     │              │
│ • Daily      │     │ • Socratic   │     │ • TodayView  │
│   lessons    │     │   tests      │     │   dashboard  │
│ • Adaptive   │     │ • Adaptive   │     │ • Messages   │
│   difficulty │     │   difficulty │     │   struggling │
│ • Code       │     │ • Plagiarism │     │   students   │
│   examples   │     │   detection  │     │ • Overrides  │
│ • Project    │     │ • DrillCard  │     │   grades     │
│   tasks      │     │   spaced     │     │              │
│              │     │   repetition │     │              │
└──────────────┘     └──────────────┘     └──────────────┘
```

**AI trains. Humans mentor. Never blur these roles.**
