# TraineesAI

**AI-driven training platform for engineering internees.**

AI teaches. AI tests. Human mentors. The training platform that takes the training burden off busy engineers and managers.

## What is this?

TraineesAI is the modernized successor to [ExaminerAI](https://github.com/fccljbplant/ExaminerAI). It's a Next.js SaaS platform designed for a specific problem in industry:

> When a new internee or trainee joins, engineers and management don't have time to train them. This platform shifts the training burden to AI — AI teaches, AI tests, AI tracks progress. The human mentor only steps in when AI flags a student needs help.

## Core model

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   AI Train   │────▶│  AI Assess   │────▶│ Human Mentor │
│              │     │              │     │              │
│ • Daily      │     │ • Socratic   │     │ • Monitors   │
│   lessons    │     │   tests      │     │   dashboard  │
│ • Code       │     │ • Project    │     │ • Messages   │
│   examples   │     │   tasks      │     │   struggling │
│ • Visual     │     │ • Weekly     │     │   students   │
│   diagrams   │     │   exams      │     │ • Overrides  │
│ • Project    │     │              │     │   grades     │
│   tasks      │     │              │     │              │
└──────────────┘     └──────────────┘     └──────────────┘
```

**AI trains. Humans mentor. Never blur these roles.**

## What's in this repo?

This repo contains the **modernization plan** for transitioning ExaminerAI → TraineesAI. The actual codebase lives in the ExaminerAI repo and will be migrated in 4 phases:

| Phase | What | Status |
|---|---|---|
| **Phase 1** | Strip the behavioral/psychological surveillance layer (~30 files, ~6,000 lines) | Planned |
| **Phase 2** | Modernize student learning (slide-based viewer + proactive AI tutor) | Planned |
| **Phase 3** | Simplify instructor experience (3 tabs: Today / Students / Messages) | Planned |
| **Phase 4** | Polish + ship (strict TypeScript, clean modules, consolidated schemas) | Planned |

See **[MODERNIZATION_PLAN.md](./MODERNIZATION_PLAN.md)** for the full execution plan.

## Why the rename?

ExaminerAI was originally built with a Socratic assessment focus. As the product evolved, it accumulated a significant behavioral/psychological monitoring layer (7-dimension psych profiling, teacher behavior surveillance, counselor role, crisis flags) that contradicts the core mission. TraineesAI represents a clean return to the original vision: **AI trains, humans mentor, no surveillance.**

## Tech stack

- **Framework**: Next.js 16 (App Router, Turbopack)
- **Database**: Prisma 6 (SQLite dev / Postgres prod)
- **AI**: DeepSeek (primary) + Z.ai GLM (fallback)
- **UI**: Tailwind 4 + shadcn/ui + Radix primitives
- **Auth**: Custom JWT + bcrypt
- **Hosting**: Vercel

## License

Proprietary. © fccljbplant.
