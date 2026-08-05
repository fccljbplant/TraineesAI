# TraineesAI Modernization — Master Plan

## Project context

TraineesAI is the modernized successor to ExaminerAI (https://github.com/fccljbplant/ExaminerAI). It's a Next.js 16 SaaS platform for training fresh engineering internees.

**The core model:** AI does the training (teaching, Socratic testing, project task generation). Instructors (busy engineers) only monitor progress and mentor struggling students via in-app messages.

**The goal of this modernization:** Remove the behavioral/psychological surveillance layer that accumulated in ExaminerAI, modernize the UX, and sharpen the AI-trains + human-mentors model.

- **Repository (source):** https://github.com/fccljbplant/ExaminerAI
- **Repository (target):** https://github.com/fccljbplant/TraineesAI
- **Tech:** Next.js 16 (App Router), Prisma 6 (SQLite dev / Postgres prod), DeepSeek AI, Tailwind 4, shadcn/ui, Vercel

---

## Non-negotiable principles

1. **AI trains. Humans mentor.** Never blur these roles.
2. **Instructors are collaborators**, not subjects to be monitored.
3. **Students are learners**, not psychological subjects.
4. Every feature must answer: *"Does this help a busy engineer mentor with minimum time?"*
5. **Never break production.** Each phase ships independently.

---

## Background: What ExaminerAI has today

### What's working well (KEEP)

- **Course-centric architecture** — clean domain-agnostic design (Course → Week → Day). Works for any subject (web dev, HR, engineering, finance).
- **AI Tutor** — well-designed teacher persona, course+project+week context injection, Roman-script language matching, short conversational replies, no grading (correct role separation from examiner).
- **Socratic testing** — practice/daily/weekly tests with conceptual questions (not MCQs), 4 pillars (Why Probe / Break-It / Client Translation / Edge Case), lenient beginner-friendly grading with 50% floor.
- **Plagiarism detection** — heuristic + AI combined (markdown artifacts, AI-typical phrasing, voice inconsistency). Useful regardless of behavioral monitoring.
- **Project-based learning** — AI generates tailored weekly task lists from project definition, Gantt chart, milestones, project reports with AI analysis.
- **Course Outline** — DB-driven, shows weeks/days with objectives, whyItMatters, topics, activities, deliverables, resources.
- **DailyTaskReminder** — well-engineered popup with localStorage persistence.
- **Self-paced learning** — `selfPacedEnabled` flag, `currentDay` advances on completion.
- **Comments + marks override** — instructor can comment on any entity + override AI's score (human-in-the-loop).
- **In-app Messages** — replaces WhatsApp, scoped to course enrollments.
- **AskMyInstructor FAB** — student can email instructor from any view.
- **Certificate generation** + verify-token for portfolio use.
- **Audit logging** — every role change, block, approve is logged.
- **RBAC + IDOR protection** — `assertCanAccessStudent` everywhere.
- **AI cost controls** — token cache, per-user rate limits, RPM/RPD caps.

### What needs to go (REMOVE)

~6,000 lines of behavioral/psychological surveillance code across ~30 files:

| Category | What it does | Why it doesn't fit |
|---|---|---|
| 7-dimension psych pipeline | Profiles students on calibration (Dunning-Kruger), mindset, cognitive load, gaming patterns, attribution, SRL phase, fluency | You're training engineers, not running a psychology clinic |
| Teacher behavior monitoring | Scans every instructor comment for "aggressive language", tracks their "load tier", monitors AI Assistant sessions | Engineers volunteering as mentors shouldn't be surveilled |
| Counselor role + crisis flags | 736-line counselor dashboard, crisis queue, wellbeing tiers, self-harm risk flags | Not your use case — this is for schools with pastoral care duties |
| Auto-generated alerts | AI analyzes student chat for "frustration", "avoidance patterns" and auto-sends messages | Instructors should decide who needs help, not an algorithm |
| Safeguarding filter | Scans every teacher→student message for abusive patterns | Treats mentors as risks, not collaborators |

---

## Phase 1: Strip the surveillance layer (removal only, no new features)

**Goal:** Remove all behavioral/psychological monitoring code without breaking the training core.

### 1.1 Delete psychological analysis engine

Remove these files entirely (they form the 7-dimension psych pipeline):

```
src/modules/assessment/lib/psych-analyzer.ts          (247 lines)
src/modules/assessment/lib/analysis-pipeline.ts        (495 lines)
src/modules/assessment/lib/engagement-tracker.ts       (343 lines)
src/components/examiner/instructor/PsychologicalTab.tsx (427 lines)
src/components/examiner/instructor/CalibrationScatterCard.tsx
src/app/api/psych-evidence/route.ts
src/app/api/confidence-ratings/route.ts
src/app/api/wellbeing-state/route.ts
src/app/api/students/alerts/route.ts
src/app/api/students/check-alerts/route.ts             (remove from vercel.json crons too)
```

Remove all imports/calls to these files from:
- `src/app/api/ai/evaluate/route.ts` — drop the `runAnalysisPipeline` call + PsychologyObs write
- `src/app/api/ai/tutor/route.ts` — drop the `trackTutorEngagement` + `analyzeMessage` calls
- `src/app/api/ai/weekly-test/route.ts` — drop psych evidence writes
- `src/app/api/ai/daily-test/route.ts`
- `src/app/api/students/[id]/generate-report-card/route.ts` — drop behavioral signal pulls
- `src/components/examiner/instructor/StudentPortfolioPage.tsx` — remove PsychologicalTab import

### 1.2 Delete teacher-behavior monitoring

Remove entirely:
```
src/components/examiner/admin/InstructorBehaviorTab.tsx  (267 lines)
src/app/api/admin/instructor-behavior/route.ts           (115 lines)
src/components/examiner/instructor/InstructorLoadPanel.tsx (212 lines)
src/app/api/instructor/load/route.ts                     (188 lines)
src/lib/ai-assistant/safeguarding.ts                     (282 lines)
src/lib/ai-assistant/escalation.ts                       (262 lines)
src/lib/ai-assistant/scope.ts
src/app/api/assistant/escalation/run/route.ts            (remove from vercel.json crons)
src/app/api/assistant/action-dialog/route.ts
```

Remove the safeguarding scan call from `src/app/api/comments/route.ts` POST handler.
Remove the "instructor-behavior" view from `AdminDashboard.tsx`.

### 1.3 Delete the Counselor role + pastoral dashboards

Remove entirely:
```
src/components/examiner/CounselorDashboard.tsx           (736 lines)
src/app/api/counselor/overview/route.ts
src/app/api/counselor/*                                  (all subroutes)
src/components/examiner/PrincipalDashboard.tsx           (600 lines)
src/app/api/principal/overview/route.ts
src/components/examiner/admin/AdminPrincipalTab.tsx      (484 lines)
src/app/api/crisis-flags/route.ts                        (242 lines)
```

Remove "counselor" from:
- `prisma/schema.prisma` User.role enum (and `prisma/schema.prod.prisma`)
- `src/lib/rbac.ts` + `src/lib/client-rbac.ts`
- `src/components/examiner/AppShell.tsx` (nav + role switcher)
- `src/components/examiner/AdminDashboard.tsx`

### 1.4 Strip psych fields from Prisma schema

**Drop these models entirely:**
- `PsychologyObs`
- `PsychEvidence`
- `ConfidenceRating`
- `WellbeingState`
- `CrisisFlag`
- `StudentHealthSummary`
- `StudentAlert`
- `CaseReview` + `CaseReviewResponse`
- `GrowthReport` (or strip `behavioralNotes` column if the rest is useful)

**Drop these columns:**
- `Interaction`: drop `cognitiveLoad`, `confidence`, `metacognitive` (KEEP `plagiarismScore` — academic integrity)
- `WeeklyTest`: drop `examinerObs`, `psychAnalysis`, `examinerComment` (KEEP `plagiarismScore`)
- `DailyTest`: drop `psychAnalysisGenerated`
- `DailyTestAnswer`: drop `confidenceRating`
- `ReportCard`: drop `workHabits`, `examinerObservations` (KEEP grades + strengths + weaknesses + nextSteps)
- `ChatSession`: drop `behavioralSignals`, `psychAnalysis`
- `MentorshipTouchpoint`: keep the model but remove alert-driven types (`alert_response`, `escalation`)

Remove the corresponding relations from the `User` model:
- `psychObs`, `confidenceRatings`, `wellbeingState`, `crisisFlags`, `psychEvidence`, `healthSummary`, `studentAlerts`

Run `npx prisma db push --accept-data-loss` on dev, then update `prisma/schema.prod.prisma` to match.

### 1.5 Rewrite AI prompts (strip behavioral instructions)

Edit `src/modules/assessment/lib/ai-prompts.ts`:

- `GLOBAL_AI_RULES`: remove rule 8 ("CRITICAL behavioral monitoring: assess the student's thinking approach critically...")
- `SHARED_EXAMINER_RULES`: remove rule 6 ("PSYCHOLOGICAL ASSESSMENT — Do NOT include behavioral observations in individual replies...")
- `weeklyTestSystemPrompt()`: remove the "PSYCHOLOGICAL ASSESSMENT" section from the final summary (the "How do they think? Do they reason logically or guess? Are they overconfident? Do they give up?" block)
- `evaluatePrompt()`: remove the entire "BEHAVIORAL MONITORING" block (cognitiveLoad, confidence, metacognitive, thinkingApproach, engagement, "CRITICAL THINKING ANALYSIS")
- `DEFAULT_REPORT_CARD_TEMPLATE`: remove `workHabits` + `examinerObservations` sections
- `DEFAULT_AI_PROMPTS.finalAnalysisPrompt`: remove "psychological analysis, examiner's observation"

Edit `src/modules/assessment/lib/ai-provider.ts`:
- Remove `translateBehavioralSignals()` + `getConfidenceMismatchLabel()` functions (lines 453-513)
- Remove their imports from `evaluate/route.ts`

### 1.6 Clean up metadata + config

- `src/app/layout.tsx`: change `metadata.description` from "7-dimension psychological cycle. AI mentorship at scale." to "AI-driven training platform for engineering internees. AI teaches, AI tests, human mentors."
- `next.config.ts`: set `typescript.ignoreBuildErrors: false` + `reactStrictMode: true`
- `vercel.json`: remove the two cron jobs (`/api/students/check-alerts`, `/api/assistant/escalation/run`)
- Delete `src/modules/wellbeing/` directory entirely

### 1.7 Verify Phase 1

- [ ] `npm run lint` → 0 errors
- [ ] `npx tsc --noEmit` → 0 errors in src/ (ignore examples/)
- [ ] `npm run build` → succeeds
- [ ] Manual test: student can take a practice question, weekly test, log check-in, work on project
- [ ] Manual test: instructor can see student roster, view portfolio, send message, override grade
- [ ] Deploy to Vercel, verify production works

---

## Phase 2: Modernize the student learning experience

**Goal:** Replace the flat course outline with a slide-based viewer + proactive AI tutor.

### 2.1 Build the SlideViewer component

Create `src/components/examiner/SlideViewer.tsx`:

- Reads a `CourseDay` from the DB
- Generates slides **on-the-fly** (NO Slide DB table) as a render function:
  - If `videoUrl` exists → **Video slide** (embedded player)
  - `objective` + `whyItMatters` → **Concept slide** (text + callout)
  - `codeExamples[]` → **Code slide** (syntax-highlighted, one per example)
  - `webImages[]` → **Visual slide** (real web image + source attribution)
  - `activity` + `deliverable` + `githubCommit` → **Activity slide** (capstone work card)
  - `reflection[]` → **Reflection slide** (end-of-day, feeds Daily Check-in)
- Horizontal flow strip at top (clickable chips: ✓ Video → ✓ Concept → 3 Code → 4 Visual → ...)
- Prev/Next nav with keyboard arrow support (← →)
- Topic strip at top (always visible): Course › Week › Day — Title

### 2.2 Add new CourseDay fields (additive, non-breaking)

Add to `prisma/schema.prisma` CourseDay model:
```prisma
videoUrl      String?   // YouTube embed URL
videoTitle    String?
codeExamples  String    @default("[]")  // JSON: [{filename, language, code, explanation}]
webImages     String    @default("[]")  // JSON: [{url, caption, source}]
```
Run `npx prisma db push`. Update GET/POST/PUT `/api/courses/[id]` to handle these fields.

### 2.3 Extend the AI course generation prompt

Edit `src/app/api/courses/generate/route.ts`:
- Add `videoSearchQuery` to the per-day instructions (YouTube search phrase)
- Add `codeExamples` (1-3 code blocks with filename, language, code, explanation)
- Add `webImages` (0-2 real diagram URLs with caption + source)
- Raise `maxTokens` cap to 30000

### 2.4 Build the proactive AI Tutor panel

Create `src/components/examiner/AIPanel.tsx`:

- Right-side persistent panel (360px on desktop, bottom sheet on mobile)
- Shows "AI is reading: [current slide name]" strip (AI knows current slide via React state)
- Conversation history carries across slides (doesn't reset)
- **Proactive bubbles** — pops after:
  - 15s idle on a code slide
  - After video ends
  - On activity slide arrival
  - Bubble content is contextual (e.g. "Notice line 8 — want me to show what happens if they shared state?")
  - Click bubble → focuses AI input with prefilled question
  - × to dismiss
- Quick-action chips: "Explain differently", "Give an example", "I'm stuck"
- Keyboard: `/` to focus input, Enter to send, Shift+Enter for newline

### 2.5 Wire SlideViewer + AIPanel into the student experience

- Replace `CourseOutline.tsx` with `SlideViewer.tsx` for students
- The AIPanel replaces the current `AITutor.tsx` when in the SlideViewer context
- Add "Learn" as the first nav item for students (replaces "Course Outline")
- Keep the old AITutor.tsx for standalone chat outside the slide context

### 2.6 Verify Phase 2

- [ ] Generate a new course with AI → verify slides render with video/code/visual/activity
- [ ] Click ✨ on individual fields in CoursePlanner → verify per-field generation works
- [ ] Navigate slides with keyboard arrows
- [ ] Verify AI bubble pops after 15s idle on a code slide
- [ ] Deploy to Vercel

---

## Phase 3: Modernize the instructor experience

**Goal:** Simplify the instructor dashboard to 3 focused tabs.

### 3.1 Simplify the instructor dashboard

Edit `src/components/examiner/TeacherDashboard.tsx` (rename to `InstructorDashboard.tsx`):

**Keep 3 tabs:**
1. **Today** — students needing attention (based on: low scores, inactivity, pending tasks — NOT psych signals), recent submissions, quick actions
2. **Students** — roster sorted by attention score (recompute attention score WITHOUT psych fields — use: last active days, latest score trend, task completion rate, test scores)
3. **Messages** — in-app messaging inbox

**Remove:**
- MentorshipView (GROW coaching)
- CaseReviewPanel
- VoiceTouchpointLogger
- InstructorRulesPanel
- InstructorLoadPanel

**Keep:**
- AssignmentsTab (group tasks + peer assessment — useful)
- InsightsTab (operational analytics, strip pastoral charts)

### 3.2 Redesign StudentPortfolioPage

Edit `src/components/examiner/instructor/StudentPortfolioPage.tsx` (1353 lines → target ~600):

**4 tabs:**
1. **Overview** — current week/day, progress %, recent activity, latest scores, quick "send message" button
2. **Academic** — test history, practice answers, competency map, report cards
3. **Project** — task list, Gantt, GitHub commits, project reports
4. **Messages** — conversation history with this student

**Remove:**
- PsychologicalTab
- MentorshipTab
- Calibration scatter
- Crisis flags
- Wellbeing tier display

### 3.3 Recompute the "attention score" without psych fields

Edit `src/app/api/stats/route.ts`:

New attention score formula:
```
attentionScore = (days_since_active * 2)
               + (low_score_count)
               + (overdue_task_count)
               + (missed_checkin_count)
```

- No psych signals
- No wellbeing tier
- No frustration/avoidance counts
- Sort instructor roster by this score descending

### 3.4 Simplify report card generation

Edit `src/app/api/students/[id]/generate-report-card/route.ts`:

- **Keep:** grade computation (weekly test 80% + practice 20%), strengths, weaknesses, nextSteps
- **Remove:** workHabits, examinerObservations, behavioral signal pulls
- The report card becomes purely academic — what they scored, what they're good at, what to improve

### 3.5 Verify Phase 3

- [ ] Instructor dashboard loads without errors
- [ ] Student portfolio shows 4 tabs (no Psychological/Mentorship)
- [ ] Attention score is computed from academic signals only
- [ ] Report card generates without psych fields
- [ ] Deploy to Vercel

---

## Phase 4: Polish + ship

**Goal:** Clean up technical debt, re-enable strict checks, ship.

### 4.1 Re-enable strict TypeScript

- `next.config.ts`: `typescript.ignoreBuildErrors: false`
- Fix any type errors that surface (there will be some from the removals)
- `reactStrictMode: true`

### 4.2 Clean up the module structure

- Delete the empty skeleton modules: `src/modules/admin/`, `src/modules/auth/`, `src/modules/communication/`, `src/modules/grading/`, `src/modules/shared/`, `src/modules/student/`, `src/modules/wellbeing/`
- Move the 1-line re-export shims in `src/lib/` (ai-provider.ts, ai-prompts.ts, course-defaults.ts) to point directly to `src/modules/assessment/lib/` and `src/modules/course/lib/` — or consolidate the files into `src/lib/` directly
- Remove the `examples/` directory (websocket demo — not part of the product)

### 4.3 Consolidate the Prisma schemas

- Ensure `prisma/schema.prisma` (SQLite dev) and `prisma/schema.prod.prisma` (Postgres) are identical except for the provider line
- Add a CI check or pre-commit hook that diffs them

### 4.4 Update branding

- Rename "ExaminerAI" → "TraineesAI" across:
  - `src/app/layout.tsx` (metadata title + description)
  - `src/components/examiner/Login.tsx` (heading)
  - `src/components/examiner/AppShell.tsx` (logo text)
  - `package.json` (name)
  - `README.md`
- Update the logo/brand mark if desired

### 4.5 Final verification

- [ ] `npm run lint` → 0 errors, minimal warnings
- [ ] `npx tsc --noEmit` → 0 errors
- [ ] `npm run build` → succeeds, ~96+ static pages
- [ ] `npm run test` → all passing
- [ ] Deploy to Vercel production
- [ ] Smoke test: student signup → AI generates course → student takes lesson → student takes test → instructor sees progress → instructor messages student → student replies

---

## Execution notes

1. **Do Phase 1 first, completely, before starting Phase 2.** The removal is the highest-risk work (lots of imports to clean up). Get it stable, deploy it, then build on top.
2. **After each phase: commit, deploy, smoke test.** Don't accumulate phases without shipping.
3. **When removing files, grep for imports first.** Use `rg "filename"` to find all references before deleting — otherwise the build will break.
4. **The Prisma migration is destructive.** Back up the production DB before running `db push --accept-data-loss`. The `--accept-data-loss` flag is required because we're dropping columns.
5. **Keep the plagiarism detection.** It's academic integrity (catching AI-generated answers), not behavioral monitoring. The `plagiarismScore` field stays on `Interaction` and `WeeklyTest`.
6. **The `MentorshipTouchpoint` model stays but simplified.** Rename to "Contact Log" — it's just instructors manually logging "I talked to this student about X". Remove all alert-driven types.
7. **Don't touch the AI Tutor's core personality.** It's well-designed (friendly teacher, Roman-Urdu support, no grading). Just remove the behavioral tracking calls, not the tutor itself.
8. **Test on mobile.** The SlideViewer + AIPanel must work on narrow screens (AI panel → bottom sheet).

---

## Success criteria

After all 4 phases:

- ✅ Codebase is ~30% smaller (surveillance layer removed)
- ✅ Student learning experience is slide-based with proactive AI
- ✅ Instructor experience is 3 tabs (Today / Students / Messages) — no pastoral dashboards
- ✅ AI prompts contain zero behavioral/psychological instructions
- ✅ Prisma schema has zero psych/wellbeing/crisis models
- ✅ Production is stable, tests pass, build succeeds with strict TypeScript
- ✅ Renamed from ExaminerAI → TraineesAI

---

## File impact summary

| Category | Files affected | Estimated lines removed/changed |
|---|---|---|
| Psych analysis engine (delete) | 10 files | ~2,000 lines removed |
| Teacher behavior monitoring (delete) | 9 files | ~1,200 lines removed |
| Counselor role + pastoral dashboards (delete) | 8 files | ~2,100 lines removed |
| Prisma schema (strip psych models/fields) | 2 files | ~200 lines removed |
| AI prompts (strip behavioral instructions) | 2 files | ~150 lines changed |
| Metadata + config cleanup | 4 files | ~20 lines changed |
| New SlideViewer + AIPanel (Phase 2) | 3 new files | ~800 lines added |
| Instructor dashboard simplification (Phase 3) | 3 files | ~1,500 lines removed/changed |
| Module structure cleanup (Phase 4) | ~15 dirs deleted | ~200 lines removed |
| **Net** | **~50 files touched** | **~6,500 lines removed, ~800 added** |

---

*This plan is based on a deep audit of the ExaminerAI codebase as of August 2026. The audit covered 118 API routes, 84 components (21,922 lines), 34 lib files, 45 module files, and a 1,002-line Prisma schema with 30+ models.*
