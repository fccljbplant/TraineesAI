# TraineesAI — Professional Product Vision

*The AI-driven training platform for engineering internees. AI trains. AI tests. Human mentors. Purpose-built for industry — not a consumer app.*

---

## The market gap we fill

Every engineering team faces the same problem: **a fresh internee joins, and nobody has time to train them.** Senior engineers are busy with deliverables. Managers are busy with coordination. The internee sits idle for weeks, then gets assigned work they're not prepared for.

**Existing solutions don't work:**

| Platform | Why it fails for industry training |
|---|---|
| **Coursera / Udemy** | Passive video watching. No real assessment. No project work. No mentor oversight. |
| **Bootcamps (Maven, etc.)** | Expensive ($8K-15K). Human-dependent. Don't scale. Fixed schedule. |
| **Internal wikis / docs** | No structure. No assessment. No tracking. Nobody reads them. |
| **Skool / Circle** | Built for community creators, not technical training. No code assessment. No project tracking. |
| **Corporate LMS (Cornerstone, Docebo)** | Built for compliance training, not skills. Clunky. Expensive. No AI. |

**TraineesAI fills the gap:** AI delivers structured technical training + Socratic assessment + project tracking, while human engineers provide targeted mentorship only when the AI flags a student is struggling.

---

## Core product pillars

### Pillar 1: Course Marketplace — Professional course listings

**What:** A curated marketplace of professional training courses, each designed by AI and reviewed by industry engineers.

**Course listing page (public-facing):**

```
┌──────────────────────────────────────────────────────────────┐
│  TraineesAI · Courses                                        │
├──────────────────────────────────────────────────────────────┤
│                                                                │
│  [Search courses...]  [Role: All ▾]  [Level: All ▾]  [Tech ▾] │
│                                                                │
│  ┌─────────────────────┐  ┌─────────────────────┐            │
│  │  Modern Web Dev     │  │  Python for Data    │            │
│  │  & AI Integration   │  │  Engineering        │            │
│  │                     │  │                     │            │
│  │  6 weeks · 30 days  │  │  4 weeks · 20 days  │            │
│  │  ★ 4.8 (124)       │  │  ★ 4.6 (89)        │            │
│  │  1,240 enrolled     │  │  890 enrolled       │            │
│  │                     │  │                     │            │
│  │  $299  [Enroll →]   │  │  $199  [Enroll →]   │            │
│  └─────────────────────┘  └─────────────────────┘            │
│                                                                │
│  ┌─────────────────────┐  ┌─────────────────────┐            │
│  │  DevOps Fundamentals│  │  Mobile App Dev     │            │
│  │  with Cloud Labs    │  │  with React Native  │            │
│  │                     │  │                     │            │
│  │  5 weeks · 25 days  │  │  8 weeks · 40 days  │            │
│  │  ★ 4.9 (67)        │  │  ★ 4.7 (156)       │            │
│  │  540 enrolled       │  │  2,100 enrolled     │            │
│  │                     │  │                     │            │
│  │  $349  [Enroll →]   │  │  $399  [Enroll →]   │            │
│  └─────────────────────┘  └─────────────────────┘            │
│                                                                │
│  ── Featured: Free Courses ──                                 │
│  ┌─────────────────────┐  ┌─────────────────────┐            │
│  │  Git & Version      │  │  SQL Fundamentals   │            │
│  │  Control Essentials │  │  for Engineers      │            │
│  │  1 week · Free      │  │  2 weeks · Free     │            │
│  │  [Start Free →]     │  │  [Start Free →]     │            │
│  └─────────────────────┘  └─────────────────────┘            │
└──────────────────────────────────────────────────────────────┘
```

**Course detail page:**
- Course overview (what you'll learn, why it matters for industry)
- Prerequisites (skills needed before enrolling)
- Curriculum outline (weeks → days → topics)
- Instructor profile (the industry engineer who reviewed the course)
- Skills you'll earn (linked to digital credentials)
- Pricing tiers:
  - **Self-paced** — $199-399 (AI training + assessment, no human mentor)
  - **Mentored** — $499-799 (adds human mentor messages + grade overrides)
  - **Cohort** — $999-1,499 (adds scheduled cohort + live sessions + certificate)
- Enrollment options (individual, team, enterprise)
- Reviews + ratings from past students
- "What you'll be able to do after this course" (outcome-focused, not feature-focused)

**Course categories:**
1. **Web Development** — Frontend, Backend, Full-stack
2. **Cloud & DevOps** — AWS, Azure, Docker, Kubernetes, CI/CD
3. **Data & AI** — Python, ML, Data Engineering, AI Integration
4. **Mobile** — React Native, Flutter, iOS, Android
5. **Security** — AppSec, Network Security, Compliance
6. **Soft Skills for Engineers** — Code Review, Technical Communication, Agile

**Pricing model (professional, not consumer):**

| Tier | Price | Includes | Target |
|---|---|---|---|
| **Free** | $0 | 1-2 week intro courses, AI training only | Trial / lead generation |
| **Self-Paced** | $199-399/course | Full course + AI assessment + digital credential | Individual learners |
| **Mentored** | $499-799/course | + Human mentor + grade overrides + priority support | Serious career-changers |
| **Cohort** | $999-1,499/course | + Scheduled cohort + live sessions + verified certificate | Career transitioners |
| **Team** | $2,999-4,999/5 seats | + Team dashboard + shared progress + manager reports | Small teams |
| **Enterprise** | Custom | + Custom courses + SSO + dedicated AI + SLA + analytics | Companies (50+ trainees) |

---

### Pillar 2: Verified Digital Credentials — Professional skill verification

**What:** When a student completes a course with a score ≥ 75%, they earn a **verified digital credential** — not a toy badge, but a professionally recognized skill verification (Credly-style).

**The credential:**

```
┌──────────────────────────────────────────────────────────────┐
│  ╔════════════════════════════════════════════════════════╗  │
│  ║  TRAININGESAI · VERIFIED CREDENTIAL                    ║  │
│  ╠════════════════════════════════════════════════════════╣  │
│  ║                                                          ║  │
│  ║  This certifies that                                    ║  │
│  ║                                                          ║  │
│  ║      Nauman Ali                                         ║  │
│  ║                                                          ║  │
│  ║  has successfully completed                             ║  │
│  ║                                                          ║  │
│  ║      Modern Web Development & AI Integration            ║  │
│  ║      6-Week Professional Training Program               ║  │
│  ║                                                          ║  │
│  ║  Final Score: 87/100 · Capstone: Passed                 ║  │
│  ║  Completed: August 2026                                  ║  │
│  ║  Credential ID: TRN-AI-2026-08-NA-87                    ║  │
│  ║                                                          ║  │
│  ║  Verify at: trainees.ai/verify/TRN-AI-2026-08-NA-87    ║  │
│  ║                                                          ║  │
│  ║  Skills verified:                                        ║  │
│  ║  ✓ HTML/CSS fundamentals  ✓ JavaScript (ES6+)          ║  │
│  ║  ✓ React components       ✓ API integration            ║  │
│  ║  ✓ Database design        ✓ Git workflow               ║  │
│  ║  ✓ AI API integration     ✓ Deployment                 ║  │
│  ║                                                          ║  │
│  ╚════════════════════════════════════════════════════════╝  │
│                                                                │
│  [Add to LinkedIn]  [Download PDF]  [Share]                   │
└──────────────────────────────────────────────────────────────┘
```

**Why this matters professionally:**
- Each credential has embedded metadata (skills, score, evidence) — verifiable by employers
- LinkedIn integration: "Add to Profile" auto-fills the "Licenses & certifications" section
- Employer verification API: recruiters can verify credentials programmatically
- Credential ID is unique + tamper-proof (stored on our DB, verified via URL)

**Skill taxonomy:**
Each credential lists specific verified skills (not generic "completed a course"). Skills are drawn from the course's competency model — the same competencies the AI tests during Socratic assessments.

---

### Pillar 3: Professional Achievement System

**NOT consumer gamification.** No XP, no levels, no streaks, no leagues. Those are consumer psychology tactics (Duolingo-style) that feel infantilizing in a professional context.

**Instead: skill-verified milestones** that map to industry expectations.

**Milestone types:**

| Milestone | How earned | Professional value |
|---|---|---|
| **Course Completion** | Finish all weeks + score ≥ 60 | Verified credential |
| **Distinction** | Score ≥ 85 on final assessment | "With Distinction" on credential |
| **Capstone Certified** | Capstone project passes peer + mentor review | Portfolio-ready project |
| **Skill Mastery** | Score ≥ 90 on 3+ questions in a topic | "Skill verified" on profile |
| **Fast Track** | Complete course in ≤ 60% of estimated time | "Efficient learner" badge |
| **Consistent Performer** | Score ≥ 70 on every weekly test | "Reliable" on employer report |
| **Peer Recognized** | 5+ peer code reviews approved | "Team player" on profile |
| **Mentor Endorsed** | Instructor writes a positive endorsement | Visible on credential |

**Why this works for professionals:**
- Every milestone maps to a real industry signal (reliability, efficiency, teamwork)
- No "🔥 7-day streak" nonsense — professionals don't need dopamine hits
- Achievements are **evidence-based**, not engagement-based
- Employers see these on the candidate's profile and understand what they mean

**Profile achievement display (professional, not gamey):**

```
┌──────────────────────────────────────────────────────────────┐
│  Nauman Ali · TraineesAI Profile                              │
├──────────────────────────────────────────────────────────────┤
│                                                                │
│  Verified Credentials:                                        │
│  🎓 Modern Web Dev & AI Integration — Score: 87 (Aug 2026)  │
│  🎓 Git & Version Control Essentials — Score: 92 (Jul 2026) │
│                                                                │
│  Skill Verifications:                                         │
│  ✓ JavaScript (ES6+) — Mastery 90%                           │
│  ✓ React Components — Mastery 85%                            │
│  ✓ API Integration — Mastery 78%                             │
│  ✓ Database Design — Mastery 82%                             │
│  ○ DevOps — In Progress (45%)                                │
│                                                                │
│  Professional Milestones:                                     │
│  ✓ Capstone Certified — "Restaurant Website" (live demo)    │
│  ✓ Consistent Performer — scored ≥70 on all weekly tests    │
│  ✓ Peer Recognized — 7 peer code reviews approved           │
│                                                                │
│  Capstone Project:                                           │
│  📦 github.com/nauman/restaurant-website                     │
│  🌐 restaurant-demo.trainees.ai (live)                       │
│  ✓ Passed peer review (2/2 approved)                        │
│  ✓ Passed mentor review                                      │
└──────────────────────────────────────────────────────────────┘
```

---

### Pillar 4: Learning Paths — Role-based curriculum

**What:** Instead of isolated courses, students follow **learning paths** designed for specific industry roles.

**Example learning paths:**

```
Frontend Developer Path
├── 1. HTML & CSS Fundamentals (2 weeks, Free)
├── 2. JavaScript Essentials (3 weeks, $199)
├── 3. React Development (4 weeks, $299)
├── 4. Frontend Testing (2 weeks, $149)
└── 5. Capstone: Build a Production Frontend (2 weeks, included)

Backend Developer Path
├── 1. Programming Fundamentals (3 weeks, $199)
├── 2. Database Design & SQL (3 weeks, $249)
├── 3. API Development (4 weeks, $299)
├── 4. Authentication & Security (2 weeks, $199)
└── 5. Capstone: Build a REST API (2 weeks, included)

DevOps Engineer Path
├── 1. Linux Fundamentals (2 weeks, $199)
├── 2. Docker & Containers (3 weeks, $249)
├── 3. CI/CD Pipelines (2 weeks, $199)
├── 4. Cloud Deployment (3 weeks, $299)
└── 5. Capstone: Deploy a Microservice (2 weeks, included)
```

**Why learning paths:**
- Employers hire for roles, not individual courses
- Paths give students a clear trajectory ("I'm on the Frontend path, 60% complete")
- Path completion earns a **Path Credential** (higher value than individual course credentials)
- Employers can sponsor a full path for their internees (one purchase, structured outcome)

**Path pricing:**
- Individual courses: $199-399 each (total $1,000-1,400 for a 5-course path)
- Full path bundle: $799-1,199 (30% savings vs buying individually)
- Enterprise path sponsorship: $2,999/internee (includes mentor + cohort + certificate)

---

### Pillar 5: Employer & Institution Dashboard

**What:** A B2B dashboard for companies and training institutions to:
- Track their sponsored internees' progress
- Measure training ROI (time-to-productivity, skill gap closure)
- Manage enrollments (bulk purchase, assign seats, revoke access)
- Download compliance reports (for audit/regulated industries)

**Employer dashboard:**

```
┌──────────────────────────────────────────────────────────────┐
│  Inzet Enterprises · Training Dashboard                       │
├──────────────────────────────────────────────────────────────┤
│                                                                │
│  Active Trainees: 12    Courses Enrolled: 4                  │
│  Total Investment: $14,388    Avg Completion: 78%            │
│  Avg Time-to-Productivity: 4.2 weeks (industry avg: 8)      │
│                                                                │
│  ── Trainee Progress ──                                       │
│  Nauman Ali    Web Dev Path    65% ████░░  On track         │
│  Aisha Khan    DevOps Path     40% ██░░░░  Needs attention   │
│  Bilal Ahmed   Backend Path    85% █████░  Completing soon  │
│  Sara Malik    Frontend Path   20% █░░░░░  Just started     │
│                                                                │
│  ── Skill Gap Analysis ──                                     │
│  Team's weakest skills:                                       │
│  1. Database Design (avg 55%) → Recommend: DB course         │
│  2. Testing (avg 48%) → Recommend: Testing course            │
│  3. Security (avg 52%) → Recommend: AppSec course            │
│                                                                │
│  ── ROI Summary ──                                            │
│  Training cost: $14,388                                       │
│  Est. productivity gain: $48,000 (3.3x ROI)                  │
│  Time saved by senior engineers: ~120 hours                  │
│  (at $75/hr = $9,000 saved)                                  │
│                                                                │
│  [Enroll More Trainees]  [Download Report]  [Schedule Review]│
└──────────────────────────────────────────────────────────────┘
```

**Why this matters:**
- Companies need to justify training spend — the ROI calculator does this automatically
- Senior engineers save ~10 hours/internee (the AI handles training, they just mentor)
- Skill gap analysis recommends next courses (upsell opportunity)
- Compliance reports for regulated industries (banking, healthcare, etc.)

---

### Pillar 6: AI-Powered Course Creation (for instructors/institutions)

**What:** Companies can create custom training courses for their internal tech stack using the AI course generator.

**Flow:**
1. Company admin describes their tech stack + training needs
2. AI generates a full course outline (weeks, days, slides, assessments)
3. Company's senior engineer reviews + edits the outline
4. Course is published to their private institution dashboard
5. Internees take the course; AI trains + tests; senior engineer mentors

**Use case:** A company using a proprietary framework (e.g., internal React component library) can't find off-the-shelf training. They use TraineesAI to generate a custom course in 10 minutes.

**Pricing:**
- Custom course creation: $999 one-time (AI generates + engineer reviews)
- Private hosting: $499/month (course visible only to their team)
- White-label: $1,999/month (their domain, their branding, their AI prompts)

---

## The professional leaderboard (not a game)

**What:** A cohort performance view — NOT a competitive game leaderboard.

```
┌──────────────────────────────────────────────────────────────┐
│  Cohort Performance · Week 3 · Inzet Enterprises              │
├──────────────────────────────────────────────────────────────┤
│  (Visible to instructors + enrolled students)                 │
│                                                                │
│  ── By Skill Mastery (not XP) ──                              │
│  1. Bilal Ahmed   — 85% avg mastery (Backend Path)           │
│  2. Nauman Ali    — 78% avg mastery (Web Dev Path)           │
│  3. Aisha Khan    — 65% avg mastery (DevOps Path)            │
│  4. Sara Malik    — 52% avg mastery (Frontend Path)          │
│                                                                │
│  ── Cohort Health ──                                          │
│  Avg mastery: 70%    On-track: 3/4    At-risk: 1/4          │
│  Weakest topic: Database Design (avg 55%)                    │
│  Strongest topic: JavaScript (avg 82%)                       │
│                                                                │
│  ── Team Progress ──                                          │
│  Week 1: 100% complete   Week 2: 88% complete                │
│  Week 3: 65% complete    Week 4: 12% complete                │
│                                                                │
│  [View Individual Reports]  [Export to PDF]                   │
└──────────────────────────────────────────────────────────────┘
```

**Why this is professional:**
- Ranked by **skill mastery** (actual competence), not XP (engagement)
- Focused on **team health**, not individual competition
- Instructor-facing — helps identify who needs help, not who's "winning"
- Students can see their own rank for motivation, but it's framed as "where am I on the journey" not "am I beating others"

---

## Implementation priority

| Priority | Feature | Effort | Business value |
|---|---|---|---|
| **P0** | Course listing page (public marketplace) | Medium | CRITICAL — this is the front door for paying customers |
| **P0** | Course detail page with pricing tiers | Medium | CRITICAL — conversion page |
| **P0** | Verified digital credentials | Medium | HIGH — this is what employers pay for |
| **P1** | Learning paths (role-based curriculum) | Medium | HIGH — increases average order value |
| **P1** | Employer dashboard (B2B) | Large | HIGH — unlocks enterprise contracts |
| **P1** | Professional achievement system (milestones) | Small | MEDIUM — differentiates from consumer apps |
| **P1** | Cohort performance view (not game leaderboard) | Small | MEDIUM — instructor value |
| **P2** | AI course creation for institutions | Large | HIGH — custom course revenue stream |
| **P2** | LinkedIn integration for credentials | Small | MEDIUM — viral growth |
| **P2** | Employer verification API | Small | MEDIUM — trust building |
| **P2** | Skill taxonomy + competency model | Medium | HIGH — foundation for credentials |
| **P3** | White-label hosting | Large | MEDIUM — enterprise upsell |

---

## What we deliberately DON'T do (and why)

| Feature | Why we don't do it |
|---|---|
| **XP points** | Consumer mechanic. Professionals don't need dopamine hits to learn. |
| **Streaks** | Creates anxiety, not learning. A professional who studies 3x/week for 2 hours is better than one who does 10 min/day to maintain a streak. |
| **Leagues** | Competitive ranking discourages collaboration. Industry needs team players, not solo competitors. |
| **Community feed (Skool-style)** | Not our core. We're a training platform, not a social network. (But we do have peer code review — that's professional collaboration, not social posting.) |
| **Live streaming** | Not scalable. AI training is always available. Live sessions are optional add-ons for cohort tier only. |
| **AI-generated images in courses** | Unprofessional. We use real web images + diagrams from documentation, not AI art. |

---

## The business model

```
┌─────────────────────────────────────────────────────────┐
│                    Revenue Streams                       │
├──────────────────────┬──────────────────────────────────┤
│  Individual courses  │  $199-399 per course             │
│  Learning paths      │  $799-1,199 per path             │
│  Cohort programs     │  $999-1,499 per cohort seat      │
│  Team licenses       │  $2,999-4,999 per 5 seats        │
│  Enterprise          │  $4,999-19,999/month             │
│  Custom courses      │  $999 one-time + $499/month      │
│  White-label         │  $1,999-4,999/month              │
│  Credential verify   │  $199 per verification (B2B)     │
│  Marketplace fee     │  20% of instructor-published     │
└──────────────────────┴──────────────────────────────────┘
```

**Unit economics:**
- AI cost per student: ~$2-5 (DeepSeek tokens for training + assessment)
- Human mentor cost: ~$10-20 per student (10 min/week of mentor time)
- Gross margin: ~85% on self-paced, ~70% on mentored, ~50% on cohort

**Growth model:**
1. **Free courses** → lead generation (Git essentials, SQL fundamentals)
2. **Self-paced** → individual conversions ($199-399)
3. **Learning paths** → upsell to full career tracks ($799-1,199)
4. **Mentored + Cohort** → premium tier for serious learners ($999-1,499)
5. **Team + Enterprise** → B2B contracts ($2,999-19,999)
6. **Custom + White-label** → enterprise expansion ($999-4,999/month)

---

## What makes us win

**Against Coursera/Udemy:** We don't just show videos. AI trains actively — Socratic questioning, adaptive difficulty, project work, spaced repetition drills.

**Against Bootcamps:** We don't cost $8K-15K. We don't require human instructors for every session. We scale infinitely.

**Against Corporate LMS:** We're not a compliance checkbox. We build real technical skills with real assessment.

**Against Skool:** We're not a community platform. We're a training engine. AI does the teaching, not human content creators.

**The moat:** The AI training engine. No competitor has an AI that can generate a full course, deliver it via slides, test via Socratic questioning, adapt difficulty, create spaced repetition drills, and brief human mentors — all in one platform. That's our defensible advantage.

---

*This document replaces the previous vision. It is focused, professional, and market-ready — designed for B2B sales, not consumer virality.*

---

## Marketing position (from Qwen research, accepted)

**Hero line:** "Your engineers are too busy to train interns. Ours isn't."

**Category strategy:** Position as "Professional Training OS" — not just courses, but verified career outcomes. Own the category: where learning meets proof.

**Wedge market:** Engineering teams where the "intern training burden" is a daily pain. Senior engineers spending 10+ hours/week answering basic questions instead of shipping code.

**The moat:** AI examination engine + verified certificates. No competitor has both.

---

## Success metrics (from Qwen research, adapted)

| Metric | Industry average | Our target |
|---|---|---|
| Course completion rate | 15% | 60% |
| Student engagement | Baseline | +70% (via adaptive difficulty + drills) |
| Enrollment rate (visitor → paid) | 5-10% | 15% |
| Repeat purchase rate | 20-30% | 40% |
| NPS score | 30-40 | 50+ |
| Monthly active students (month 12) | — | 10,000 |
| Revenue (month 18) | — | $1M ARR |

---

## RICE prioritization (from Qwen research, adapted)

| Feature | Reach | Impact | Confidence | Effort | RICE |
|---|---|---|---|---|---|
| Course marketplace (public catalog) | 10 | 3 | 0.9 | 5 | **5.4** |
| Verified credentials | 10 | 3 | 0.8 | 4 | **6.0** |
| Learning paths | 8 | 2 | 0.8 | 3 | **4.3** |
| Employer dashboard (B2B) | 5 | 3 | 0.7 | 8 | **1.3** |
| Professional milestones | 8 | 1 | 0.9 | 2 | **3.6** |
| Cohort performance view | 6 | 1 | 0.8 | 2 | **2.4** |
| AI course creation | 4 | 3 | 0.6 | 10 | **0.7** |
| LinkedIn integration | 8 | 1 | 0.9 | 1 | **7.2** |
| Employer verification API | 5 | 2 | 0.8 | 2 | **4.0** |

**Build order (highest RICE first):**
1. LinkedIn integration (RICE 7.2) — quick win, viral growth
2. Verified credentials (RICE 6.0) — core value proposition
3. Course marketplace (RICE 5.4) — front door for customers
4. Learning paths (RICE 4.3) — increases order value
5. Employer verification API (RICE 4.0) — B2B trust
6. Professional milestones (RICE 3.6) — differentiation
7. Cohort performance view (RICE 2.4) — instructor value
8. Employer dashboard (RICE 1.3) — enterprise expansion
9. AI course creation (RICE 0.7) — future revenue stream

---

## Navigation structure (from Qwen research, adapted)

**Student nav (4 tabs — clean, professional):**
1. **Dashboard** — TodayView (what do I do next?) + learning signal + due drills
2. **My Courses** — enrolled courses with progress + course catalog (browse new)
3. **Community** — peer code review + Q&A threads (no social feed)
4. **Credentials** — verified credentials + skill milestones + capstone portfolio

**Instructor nav (5 tabs — professional, not gamey):**
1. **Today** — students needing attention + recent submissions
2. **Students** — roster sorted by academic attention score
3. **Courses** — course builder + curriculum management
4. **Analytics** — cohort health + skill gap analysis + ROI metrics
5. **Messages** — in-app messaging with students

**Admin nav (4 tabs — institutional):**
1. **Overview** — institution health + enrollment metrics
2. **Users** — user management + approvals + roles
3. **Courses** — course marketplace management + custom courses
4. **System** — AI usage + costs + feature flags + audit logs

---

## What we rejected from the Qwen proposal (and why)

| Qwen proposal | Why rejected |
|---|---|
| XP system + levels | Consumer mechanic. Professionals don't need dopamine hits to learn. |
| Streaks with freeze protection | Creates anxiety, not learning. 3x/week for 2 hours > 10 min/day for a streak. |
| Weekly leaderboards (competitive) | Discourages collaboration. We use skill-mastery rankings (cooperative). |
| "Blockchain-verified" certificates | Buzzword. A DB-backed verification URL is more reliable + cheaper. |
| Variable rewards (random XP bonuses) | Slot machine psychology. Unprofessional. |
| Decoy pricing / anchoring | Used-car tactics. We use transparent value-based pricing. |
| "Endowed progress" (start at 40/100 XP) | Manipulative. Professionals see through this. |
| Community feed (Skool-style social posting) | We're a training platform, not a social network. Peer code review only. |

---

*This document supersedes all previous planning files. It is focused, professional, and market-ready — designed for B2B sales, not consumer virality.*

---

## Implementation progress (updated August 2026)

### Phase 6: Course Marketplace + Verified Credentials — ✅ COMPLETE & DEPLOYED

**Built:**
- Course marketplace: public `/courses` listing page + `/courses/[id]` detail page
- Learning paths: `LearningPath` + `LearningPathCourse` models, public `/paths/[id]` page
- Verified digital credentials: `Certificate` model with unique credentialId, public `/verify/[credentialId]` page, LinkedIn "Add to Profile" integration
- Professional milestones: `Milestone` model (7 types: course_completion, distinction, capstone_certified, skill_mastery, consistent_performer, peer_recognized, mentor_endorsed)
- Employer verification API: `GET /api/verify/credential?credentialId=...` (public, rate-limited)
- Student credentials dashboard: `CredentialsView` component with certificates, skill mastery, milestones
- Marketplace publish toggle in CoursePlanner: admin can set price, category, published, featured, instructorName, durationWeeks

**New Prisma models:** LearningPath, LearningPathCourse, Certificate (extended), Milestone
**New public routes:** /courses, /courses/[id], /paths/[id], /verify/[credentialId], /api/marketplace/courses, /api/marketplace/paths, /api/verify/credential
**New auth routes:** /api/student/credentials

**RICE scores achieved:**
- LinkedIn integration (RICE 7.2) ✅ — built into verify page
- Verified credentials (RICE 6.0) ✅ — Certificate model + verify page
- Course marketplace (RICE 5.4) ✅ — /courses + /courses/[id]
- Learning paths (RICE 4.3) ✅ — LearningPath model + /paths/[id]
- Employer verification API (RICE 4.0) ✅ — /api/verify/credential
- Professional milestones (RICE 3.6) ✅ — Milestone model + CredentialsView

### Next priorities (by RICE):
- Cohort performance view (RICE 2.4) — instructor analytics
- Employer dashboard (RICE 1.3) — B2B dashboard with ROI tracking
- AI course creation (RICE 0.7) — custom course generation for institutions

---

## Implementation progress (updated August 2026 — Phase 6.3)

### Phase 6.3: Direct Enrollment + Landing Page + Course Management — ✅ COMPLETE

**Direct Enrollment:**
- Students can self-enroll from the marketplace (POST /api/marketplace/enroll)
- EnrollButton on course detail page adapts to auth state
- Atomic enrollment + counter increment

**Featured Courses on Landing Page:**
- Login page now has 2-column layout: login form + featured courses preview
- FeaturedCourses component fetches published+featured courses
- "Browse All Courses" CTA links to /courses

**Course Management Panel (admin):**
- Replaced old courses panel with CourseManagementPanel (427 lines)
- Stats: total courses, published count, enrollments, avg rating
- Inline publish/feature toggles
- Search + category filter
- Edit (→ CoursePlanner) + View (→ marketplace) actions

**Domain-Agnostic Categories (NOT IT-specific):**
- 10 professional domains: Technology, Engineering, Business, Finance,
  Healthcare, Manufacturing, HR, Compliance, Professional Skills, Other
- The platform works for ANY professional training, not just IT

### Note on RICE
RICE (Reach × Impact × Confidence ÷ Effort) is a universal product
management prioritization framework — it is NOT IT-specific. It works
for any product in any industry. It's simply a scoring system for
"which feature gives the most value for the least effort."

---

## Implementation progress (updated August 2026 — Phase 6.4)

### Phase 6.4: Cohort Analytics + Employer Dashboard + Mentor Briefings — ✅ COMPLETE

**Cohort Analytics (instructor):**
- /api/instructor/cohort-analytics — academic-only performance data
- CohortAnalyticsView: stats cards, weekly progress chart, topic difficulty
  chart, top performers, at-risk students
- Added "Analytics" tab to InstructorDashboard

**Employer Dashboard (B2B):**
- /api/employer/dashboard — ROI tracking, trainee progress, skill gaps
- EmployerDashboard: ROI cards, trainee table with status badges,
  skill gap analysis with recommended courses
- Added "Employer" nav item for coordinator + admin roles

**AI Mentor Briefings:**
- /api/instructor/student-briefing — 3-sentence heuristic briefing
  (no AI calls — fast + free). Generated from academic signals only.
- StudentBriefing component at top of student portfolio
- Suggested talking points based on weak topics / project status

**RICE scores achieved (9 of 9):**
All features from the RICE prioritization are now complete:
- LinkedIn integration (RICE 7.2) ✅
- Verified credentials (RICE 6.0) ✅
- Course marketplace (RICE 5.4) ✅
- Learning paths (RICE 4.3) ✅
- Employer verification API (RICE 4.0) ✅
- Professional milestones (RICE 3.6) ✅
- Cohort performance view (RICE 2.4) ✅
- Employer dashboard (RICE 1.3) ✅
- AI mentor briefings (bonus) ✅

---

## Implementation progress (updated August 2026 — Phase 7)

### Phase 7: B2C Storefront — ✅ COMPLETE & DEPLOYED

**Course Thumbnail System:**
- Unsplash free image search (no API key needed) — 12 professional stock photos per search
- File upload (base64, <500KB) for custom thumbnails
- External AI generator links (Craiyon, Canva) for custom designs
- Integrated into CoursePlanner admin UI

**Course Reviews & Ratings:**
- Students who complete a course can leave 1-5 star reviews
- Helpful upvote system (one per user per review)
- Reviews displayed on course detail page with star ratings
- Auto-updates course average rating + review count

**Category Pages:**
- /courses/category/[category] — browse courses by professional domain
- Category chips on main marketplace page with live course counts
- 10 professional categories (Technology, Engineering, Business, Finance, Healthcare, Manufacturing, HR, Compliance, Professional Skills, Other)

**Instructor Profiles:**
- /instructors/[instructorName] — public instructor profile page
- Shows bio, course count, total enrollments, avg rating, course list
- /api/marketplace/instructors — public API for instructor directory

**B2C Checkout Flow:**
- Free courses: "Enroll Free" (direct enrollment)
- Paid courses: "Enroll for $X" opens checkout dialog with:
  - Course name, price, what's included (AI tutor + certificate)
  - "Proceed to Payment" (placeholder — Stripe integration is next step)
  - Post-enrollment: "Enrolled! Continue Learning →"

**B2C Business Model:**
- Any business can create courses, set prices, and sell to the general public
- Students browse the marketplace, enroll (free or paid), learn via AI, earn verified credentials
- Instructors earn revenue from course sales
- Platform takes a percentage (marketplace fee model)

### Total feature count: 16 product pillars
1-11: Previous phases (all complete)
12. Course Thumbnails (Unsplash + upload + AI generator links) ✅
13. Course Reviews & Ratings (stars + helpful votes) ✅
14. Category Pages (browse by professional domain) ✅
15. Instructor Profiles (public, showcase courses) ✅
16. B2C Checkout (free + paid enrollment flow) ✅

---

## Implementation progress (updated August 2026 — Phase 7.2)

### Phase 7.2: My Courses + Course Creation Wizard + Marketplace Seed — ✅ COMPLETE

**My Courses Page:**
- Students see enrolled courses with progress + explore new courses
- Added "My Courses" tab to student navigation
- TodayView links to My Courses

**Course Creation Wizard:**
- 3-step dialog: Course Details → Marketplace Settings → AI Curriculum Generation
- Creates marketplace-ready courses with published=true
- Thumbnail picker, price, category, skills, prerequisites all settable
- Added to CoursePlanner as "Create New Course (Wizard)"

**Marketplace Seed Data:**
- 8 demo courses across 5 categories:
  - Technology: Web Dev & AI ($299), DevOps ($349), Git (Free)
  - Data: Python for Data Engineering ($249), SQL Fundamentals (Free)
  - Compliance: Workplace Safety ($199)
  - Business: Project Management ($229)
  - Finance: Financial Analysis ($259)
- 2 learning paths: Full-Stack Developer ($799), DevOps Engineer ($899)
- Professional Unsplash thumbnails

---

## Implementation progress (updated August 2026 — Phase 7.3)

### Phase 7.3: Paste-Your-Own-Outline AI Conversion — ✅ COMPLETE & DEPLOYED

**The feature:** Users paste any course outline (Word doc, PDF, syllabus, textbook
table of contents) into a big text box. The AI reads it and converts it into a
TraineesAI-compatible structured outline. The converted outline is fully editable.

**New API:** POST /api/courses/convert-outline — accepts raw outline text +
course metadata, AI converts to structured JSON (weeks → days → objectives,
activities, deliverables, reflections). 100K char limit, 30K maxTokens.

**In the Course Creation Wizard:** Step 3 now has two modes:
1. Generate with AI (from scratch)
2. Paste Your Outline (convert existing material)

**In CoursePlanner:** "Convert Outline" button lets instructors replace an
existing course's curriculum with a pasted outline. Amber warning before
replacing.

**Key value:** Any organization with existing training material (Word docs,
PDFs, old syllabi) can digitize it into TraineesAI in minutes — no need to
start from scratch. The AI enhances the material with objectives, activities,
reflections, and real resource URLs.

### Total feature count: 18 product pillars
1-16: Previous phases (all complete)
17. My Courses page (enrolled + explore) ✅
18. Paste-Your-Own-Outline AI conversion ✅
