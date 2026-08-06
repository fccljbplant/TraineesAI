# TraineesAI

**AI-driven training platform for engineering internees.**

AI teaches. AI tests. Human mentors. The training platform that takes the training burden off busy engineers and managers.

## What is this?

TraineesAI is the modernized successor to [ExaminerAI](https://github.com/fccljbplant/ExaminerAI). It's a Next.js SaaS platform designed for a specific problem in industry:

> When a new internee or trainee joins, engineers and management don't have time to train them. This platform shifts the training burden to AI — AI teaches, AI tests, AI tracks progress. The human mentor only steps in when AI flags a student needs help.

## Modernization status

| Phase | What | Status |
|---|---|---|
| **Phase 1** | Strip behavioral/psychological surveillance layer (~2,368 lines removed) | ✅ Complete & deployed |
| **Phase 2** | Modern training engine core (adaptive difficulty, learning signal, JSON mode, drills, TodayView) | ✅ Complete & deployed |
| **Phase 3** | Slide viewer + proactive AI tutor | ⏳ Planned |
| **Phase 4** | Simplify instructor experience (3 tabs) | ⏳ Planned |
| **Phase 5** | Polish + ship (rename, consolidate, verify) | ⏳ Planned |

See **[MODERNIZATION_PLAN.md](./MODERNIZATION_PLAN.md)** for the full execution plan with progress tracking.

## What was removed (Phase 1)

- 11 Prisma models (PsychologyObs, PsychEvidence, WellbeingState, CrisisFlag, StudentAlert, etc.)
- Counselor + Guardian roles entirely
- 7-dimension psych profiling pipeline
- Teacher behavior monitoring (safeguarding filter, InstructorBehaviorTab)
- All behavioral instructions from AI prompts

## What was added (Phase 2)

- **Adaptive difficulty engine** — 5 levels that move with scores + explicit confidence
- **Transparent Learning Signal** — 0-100 from academic facts only, shown to trainee
- **JSON mode + zod** — replaces brittle text parsing, no more silent AI failures
- **DrillCard spaced repetition** — wrong answers come back until mastered
- **TodayView** — one screen answering "what do I do next?"
- **Visible degraded mode** — AI failures are shown, not hidden

## Tech stack

- **Framework**: Next.js 16 (App Router, Turbopack)
- **Database**: Prisma 6 (SQLite dev / Postgres prod)
- **AI**: DeepSeek (primary) + Z.ai GLM (fallback)
- **UI**: Tailwind 4 + shadcn/ui + Radix primitives
- **Auth**: Custom JWT + bcrypt
- **Hosting**: Vercel

## License

Proprietary. © fccljbplant.
