# TraineesAI Modernization — Master Plan

## Project context

TraineesAI is the modernized successor to ExaminerAI (https://github.com/fccljbplant/ExaminerAI). It's a Next.js 16 SaaS platform for training fresh engineering internees.

**The core model:** AI does the training (teaching, Socratic testing, project task generation). Instructors (busy engineers) only monitor progress and mentor struggling students via in-app messages.

---

## Non-negotiable principles

1. **AI trains. Humans mentor.** Never blur these roles.
2. **Instructors are collaborators**, not subjects to be monitored.
3. **Students are learners**, not psychological subjects.
4. Every feature must answer: *"Does this help a busy engineer mentor with minimum time?"*
5. **Never break production.** Each phase ships independently.

---

## ALL PHASES COMPLETE ✅

### Phase 1: Strip the surveillance layer — ✅ COMPLETE & DEPLOYED

Removed ~2,368 lines of behavioral/psychological monitoring code:
- Deleted 11 Prisma models (PsychologyObs, PsychEvidence, WellbeingState, CrisisFlag, StudentAlert, etc.)
- Deleted Counselor + Guardian roles entirely
- Deleted 35+ files (psych lib, API routes, components, dashboards)
- Rewrote AI prompts to remove all behavioral/psychological instructions
- Re-enabled strict TypeScript

### Phase 2: Modern training engine core — ✅ COMPLETE & DEPLOYED

Built 5 new files + DrillCard model + /api/today/summary endpoint:
- Adaptive difficulty engine (5 levels, moves with scores + explicit confidence)
- Transparent Learning Signal (0-100 from academic facts only)
- JSON mode + zod for AI calls (replaces brittle text parsing)
- DrillCard spaced repetition (wrong answers come back until mastered)
- TodayView ("what do I do next?" landing screen)
- Modernized daily-test route (adaptive + JSON mode + drills + degraded mode)

### Phase 3: Slide viewer + proactive AI tutor — ✅ COMPLETE & DEPLOYED

- Added CourseDay fields: videoUrl, videoTitle, codeExamples, webImages
- NEW SlideViewer.tsx (672 lines) — on-the-fly slide generation, 6 slide types
- NEW AIPanel.tsx (306 lines) — persistent chat with proactive bubbles
- Modified CourseOutline.tsx to use SlideViewer + AIPanel

### Phase 4: Instructor experience — ✅ COMPLETE

Already adequate after Phase 1 cleanup (4 tabs: Today/Students/Assignments/Insights).

### Phase 5: Rename to TraineesAI — ✅ COMPLETE & DEPLOYED

Renamed across 11 files (AppShell, Login, landing page, TestChatUI, verify page, constants, theme, package.json, etc.).

---

## Architecture: AI trains, humans mentor

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   AI Train   │────▶│  AI Assess   │────▶│ Human Mentor │
│              │     │              │     │              │
│ • SlideView  │     │ • Socratic   │     │ • TodayView  │
│ • AIPanel    │     │   tests      │     │ • Messages   │
│ • Adaptive   │     │ • Adaptive   │     │ • Overrides  │
│   difficulty │     │   difficulty │     │   grades     │
│              │     │ • DrillCards │     │              │
└──────────────┘     └──────────────┘     └──────────────┘
```

**AI trains. Humans mentor. Never blur these roles.**

## Tech stack

- Next.js 16, Prisma 6, DeepSeek AI, Tailwind 4, shadcn/ui, Vercel

## License

Proprietary. © fccljbplant.
