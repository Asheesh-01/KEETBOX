# KEETBOX — Master Requirements Document

**Version:** 1.0
**Author:** Asheesh Sharma
**Mentor:** Better DeepSeek
**Date:** October 2026
**Status:** Locked — v1 scope confirmed

---

## Table of Contents

1. [Product Vision & Problem Statement](#1-product-vision--problem-statement)
2. [MVP Scope Document](#2-mvp-scope-document)
3. [User Flows](#3-user-flows)
4. [Tech Stack](#4-tech-stack)
5. [Architecture Decisions](#5-architecture-decisions)
6. [Security Requirements](#6-security-requirements)
7. [Supabase Setup Guide](#7-supabase-setup-guide)
8. [Folder Structure](#8-folder-structure)
9. [Nine-Week Timeline](#9-nine-week-timeline)
10. [Week 1 Daily Tasks](#10-week-1-daily-tasks)
11. [Daily Workflow](#11-daily-workflow)
12. [Appendix](#12-appendix)

---

## 1. Product Vision & Problem Statement

### 1.1 The Problem

Beginner cybersecurity students face three barriers when starting out:

- **Information overload.** Hundreds of resources, courses, and certifications exist. No one tells a beginner which path to take or why.
- **No community support.** Learning security is isolating. Beginners have questions but no safe place to ask without feeling stupid.
- **No proof of work.** Students complete tutorials but have nothing to show. Unlike GitHub for developers, no public portfolio system exists for cybersecurity students.

### 1.2 Target Users

**Primary (v1 focus):** Beginners who do not know what cybersecurity is, whether it is right for them, how to learn it, or what roadmap to follow.

**Secondary (future versions):** Intermediate and advanced students who need structured lab content, advanced roadmaps, and higher-level community support.

### 1.3 The Unique Angle

- **Beginner-first design.** Every page, note, and roadmap is written for someone with zero background. No assumed knowledge.
- **Community-driven learning.** Users shape the platform through feedback. The site evolves based on real student needs, not guesses.
- **Public portfolio for security students.** A profile system like GitHub or LinkedIn, purpose-built for cybersecurity. Shows learning graphs, streaks, and completed labs.

### 1.4 Business Model

- **v1 (current):** 100% free. No paid tiers. No ads. No monetization.
- **Future (v1.1+):** Freemium. Free tier includes community, questions, roadmap, and basic notes. Paid tier includes advanced labs, advanced roadmap, and advanced courses.
- **v1 commitment:** The homepage will say "free while in beta" — honest language that protects against bait-and-switch when the paid tier launches.

---

## 2. MVP Scope Document

### 2.1 Scope Principles

- **Security is never compromised.** Every feature built with proper auth, authorization, and input validation. No shortcuts.
- **UI quality is never compromised.** No vibecoded design. Distinct visual identity. Every design decision has a reason.
- **Legal pages ship from Day 1.** Terms of Service and Privacy Policy are not afterthoughts.

### 2.2 In Scope for v1

**Authentication & Users**
- Email + password registration
- Email verification via OTP (6-digit, 10-min expiry, max 5 attempts)
- Google OAuth sign-in
- Forgot password flow (email link, 1-hour expiry)
- Session persistence across reloads
- Global state sync (login state consistent across all pages)
- Basic profile page (name, email, avatar, bio, joined date)

**Content (Public — no login required)**
- Homepage: hero, pitch, featured notes, feedback CTA
- Roadmap page (read-only)
- Notes index (filterable by category)
- Individual note pages (markdown rendered)
- About page
- Contact / feedback form
- Terms of Service page
- Privacy Policy page

**Admin CMS (Admin only)**
- Admin dashboard (protected route)
- Create / edit / delete notes
- Create / edit / delete roadmap entries
- View users (read-only)
- Feedback inbox

**Onboarding**
- Single welcome modal on first login
- Link to a "How to use KEETBOX" page

### 2.3 Out of Scope for v1 (Backlog)

- Public profile showcase with graphs and streaks
- Course completion tracking
- Per-tab onboarding popups
- Q&A community section
- Comments on notes
- Search
- Dark mode toggle
- Payments / subscription system
- AI-powered features
- Gamification (points, badges)

### 2.4 v1.1 Sketch

- Reader accounts (post questions and comments)
- Public Q&A community section
- Streak tracking on profiles
- Basic progress visualization
- Better onboarding (guided tour)

### 2.5 v2 Sketch

- Public portfolio pages (GitHub-style for cyber students)
- Advanced labs gated behind subscription
- Advanced roadmap tracks
- Full course system with video + labs
- Community contributions (user-submitted notes and labs)

---

## 3. User Flows

### 3.1 First-Time Visitor

1. Lands on homepage
2. Sees hero section: what KEETBOX is, why it exists, who it is for
3. Sees "Sign in" and "Register" buttons in top-right nav
4. Can browse roadmap and notes without logging in

### 3.2 Registration Flow (Email + Password)

1. User clicks "Register"
2. Enters first name, last name, email
3. System sends 6-digit OTP to that email
4. User enters OTP on verification page
5. If OTP correct, user lands on "Create Password" page
6. User enters password and confirms
7. Account created. User logged in automatically
8. Welcome modal appears

### 3.3 Registration Flow (Google OAuth)

1. User clicks "Continue with Google"
2. Google consent screen appears
3. User authorizes
4. Account created automatically with Google profile data
5. User logged in. Welcome modal appears

### 3.4 Login Flow

1. User clicks "Sign in"
2. Enters email + password OR clicks "Continue with Google"
3. If credentials correct, user is logged in
4. Nav bar updates — "Sign in"/"Register" replaced with avatar dropdown
5. All pages now show logged-in state

### 3.5 Forgot Password Flow

1. User clicks "Forgot password?" on login page
2. Enters email address
3. System sends password reset link to email
4. User clicks link, opens reset page
5. User enters new password and confirms
6. User redirected to login with success message

**Alternative:** Logged-in user can change password from profile settings.

### 3.6 Global State Synchronization

- **Login state:** If user logs in on any page, every other page immediately reflects logged-in state.
- **User data:** Name, avatar, role shown in nav and profile must match database at all times.
- **Progress data (v1.1+):** Streaks, completed labs, graphs update everywhere the moment they change.

---

## 4. Tech Stack

The stack is locked. Every tool has a reason. Do not add tools without removing one.

| Layer | Tool | Why |
|-------|------|-----|
| Framework | Next.js 15 (App Router) | React-based, SEO-friendly, one-click Vercel deploy |
| Language | TypeScript | Catches bugs before runtime |
| Styling | Tailwind CSS v4 | Utility-first, no separate CSS files |
| UI Components | shadcn/ui (selective) | Copy-paste components, you own the code |
| Auth | Supabase Auth | Hashing, sessions, OAuth. Free tier |
| Database | Supabase Postgres | 500 MB free tier |
| Email | Resend | 3,000 emails/month free. OTP + notifications |
| Hosting | Vercel | Free tier. Auto-deploys from GitHub |
| Version Control | GitHub | Public repo under Asheesh-01 |
| IDE | VS Code (clean) | No AI agents inside the editor |
| AI Assistant | DeepSeek web + Gemini CLI | One task, one tool |
| Forms | React Hook Form + Zod | Client + server validation |
| State Sync | React Context + TanStack Query | Solves the "login button still showing" bug |

**Total monthly cost:** ₹0. Every tool has a free tier that covers v1 traffic.

---

## 5. Architecture Decisions

### 5.1 Global State Synchronization

**The problem:** In single-page applications, different parts of the site can show stale data. A user logs in but the nav bar still shows "Sign in" until refresh. This is the bug you experienced before.

**The solution has three layers:**

- **Layer 1 — Server-side session:** Supabase Auth Helpers check the session on every server render. Logged-in users get logged-in UI on first paint.
- **Layer 2 — Client-side context:** A single AuthProvider wraps the app. All components read auth state from this provider. State changes trigger re-renders everywhere.
- **Layer 3 — Cache invalidation:** TanStack Query handles re-fetching and cache invalidation. When a mutation happens, affected queries refresh across the app.

**Order matters:** Set this up on Day 1. Retrofitting state management later is painful.

### 5.2 Role-Based Access Control (RBAC)

- **admin:** Full access. Manages notes, roadmap, users, feedback. Only you in v1.
- **user:** Standard reader. Views public content, submits feedback, edits own profile.
- **Future roles:** subscriber (paid tier). The role column exists from Day 1 to avoid schema rewrites later.

### 5.3 Row Level Security (RLS)

RLS is Supabase's built-in access control. Every table gets policies that say who can read, insert, update, or delete each row.

**Golden rule:** RLS enabled on every table. No exceptions. If even one table has RLS disabled, its data is public to anyone with the publishable key.

### 5.4 Folder Structure Philosophy

- `src/app/` — pages and API routes
- `src/components/` — reusable UI
- `src/lib/` — utilities, Supabase clients, validation
- `supabase/migrations/` — version-controlled schema
- `docs/` — project documentation

---

## 6. Security Requirements

### 6.1 Authentication

- **Password hashing:** Supabase uses bcrypt. You never see plaintext. Never log it.
- **Session cookies:** HttpOnly, Secure, SameSite=Lax. Set by Supabase.
- **Rate limiting on login:** Max 5 failed attempts per email per 15 min. Default in Supabase — do not disable.
- **OTP expiry:** 6-digit code expires in 10 min. Max 5 attempts.
- **Password reset tokens:** Single-use, expire after 1 hour.
- **OAuth flow:** Handled by Supabase. Never store OAuth tokens in localStorage.

### 6.2 Authorization

- **Every /admin route:** Protected by server-side middleware. No session = redirect to /login.
- **Every API route:** Validates input with Zod. Rejects requests without proper session.
- **Every database table:** RLS enabled. Policies written, tested, verified.
- **Role checks:** Never trust the client. Role verified server-side on every privileged action.

### 6.3 Input Validation

- **All forms:** Validated with Zod on client and server.
- **Feedback form:** Max 2,000 characters. HTML stripped before storage (prevents XSS). Rate limited to 3 per IP per hour.
- **Email fields:** Validated against RFC 5322 format.

### 6.4 Headers & Transport

- **HTTPS:** Enforced by Vercel.
- **Content Security Policy:** Configured in next.config.ts.
- **X-Frame-Options:** DENY. Prevents clickjacking.
- **X-Content-Type-Options:** nosniff. Prevents MIME sniffing.
- **Referrer-Policy:** strict-origin-when-cross-origin.

### 6.5 Secrets Management

- **Environment variables:** Stored in .env.local (never committed) and Vercel dashboard (production).
- **.env.example:** Documents variable names, not values. Committed to Git.
- **Never log secrets:** Not passwords, tokens, or API keys. Not even in development.
- **Publishable keys:** Safe in frontend code ONLY because RLS is enabled. Verify RLS before launch.

### 6.6 Security Testing Checklist

- [ ] Access /admin without login — should redirect
- [ ] Read private DB rows via Supabase API — should return empty
- [ ] 10 failed logins — should be rate limited
- [ ] 5 feedback messages in 1 minute — should be rate limited
- [ ] HTML in feedback — should be stripped
- [ ] Verify .env.local is gitignored: `git check-ignore .env.local`
- [ ] Run `npm audit` — fix high/critical vulnerabilities

---

## 7. Supabase Setup Guide

### 7.1 Create the Project

1. Go to database.new
2. Sign in with GitHub (Asheesh-01 account)
3. Click "New Project"
4. Name: `keetbox`
5. Database Password: strong one, saved in your password manager
6. Region: Southeast Asia (Singapore)
7. Click "Create new project", wait ~2 minutes

### 7.2 Get Your Keys

1. In the dashboard, click "Connect" at the top
2. Copy Project URL (https://xxxxx.supabase.co)
3. Copy Publishable Key (starts with `sb_publishable_`)

### 7.3 Create .env.local

In the project root, create `.env.local` with:

```

NEXT_PUBLIC_SUPABASE_URL=your-project-url-here
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=sb_publishable_...

```

**Critical:** `.env.local` is in `.gitignore` by default. Verify before committing.

### 7.4 Why the Publishable Key Is Safe

The publishable key lives in frontend code because RLS is enabled. Without RLS, anyone with the key could read the entire database. With RLS, the key identifies your project, and every request is checked against your policies.

**Rule:** RLS on every table. No exceptions.

### 7.5 Auth Configuration

- Authentication → Providers: Email enabled (default)
- Enable Google provider — needs a Google Cloud OAuth client (Week 3)
- Authentication → URL Configuration:
  - Site URL: production URL (e.g., `https://cyberdragons.in`)
  - Redirect URLs: `http://localhost:3000/**` and production URL with `/**`

### 7.6 Schema Overview

- **profiles:** Extends `auth.users` with role, bio, avatar_url, created_at
- **notes:** id, title, slug, content, category, visibility, created_at, updated_at, author_id
- **roadmap_entries:** id, volume, day, title, description, order_index
- **feedback:** id, name, email, message, ip_address, user_agent, created_at, status

Every table has RLS enabled and policies written. Full SQL lives in `supabase/migrations/001_initial_schema.sql`.

---

## 8. Folder Structure

```

keetbox/
├── .env.example
├── .env.local (gitignored)
├── .gitignore
├── README.md
├── package.json
├── next.config.ts
├── tsconfig.json
├── tailwind.config.ts
├── postcss.config.mjs
├── docs/
│   ├── 00-master-plan.md
│   ├── 01-daily-log.md
│   ├── 02-backlog.md
│   ├── 03-decisions.md
│   └── weekly/
│       └── W01.md
├── public/
│   ├── logo.svg
│   └── favicon.ico
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── roadmap/page.tsx
│   │   ├── notes/page.tsx
│   │   ├── notes/[slug]/page.tsx
│   │   ├── about/page.tsx
│   │   ├── contact/page.tsx
│   │   ├── terms/page.tsx
│   │   ├── privacy/page.tsx
│   │   ├── login/page.tsx
│   │   ├── register/page.tsx
│   │   ├── verify-otp/page.tsx
│   │   ├── forgot-password/page.tsx
│   │   ├── profile/page.tsx
│   │   ├── admin/
│   │   │   ├── dashboard/page.tsx
│   │   │   ├── notes/
│   │   │   ├── roadmap/
│   │   │   ├── users/page.tsx
│   │   │   └── feedback/page.tsx
│   │   └── api/
│   │       ├── auth/callback/route.ts
│   │       ├── feedback/route.ts
│   │       └── otp/route.ts
│   ├── components/
│   │   ├── ui/
│   │   ├── nav.tsx
│   │   ├── footer.tsx
│   │   ├── feedback-form.tsx
│   │   ├── welcome-modal.tsx
│   │   └── auth-provider.tsx
│   ├── lib/
│   │   ├── supabase/
│   │   │   ├── client.ts
│   │   │   ├── server.ts
│   │   │   └── middleware.ts
│   │   ├── validations.ts
│   │   └── utils.ts
│   └── middleware.ts
└── supabase/
└── migrations/
└── 001_initial_schema.sql

```

---

## 9. Nine-Week Timeline

At 4 hours/day, 6 days/week. Total: 216 hours.

| Week | Phase | Deliverable |
|------|-------|-------------|
| 1 | Shell | Next.js + TypeScript + Tailwind running, deployed to Vercel, layout with nav + footer |
| 2 | Public Pages | Home, About, Terms, Privacy, Contact form (DB only, no email yet) |
| 3 | Auth Part 1 | Supabase project, profiles table, email + password signup with OTP |
| 4 | Auth Part 2 | Google OAuth, forgot password, session persistence, global state sync |
| 5 | Notes System | Notes index, note detail page, markdown rendering, categories |
| 6 | Roadmap + Feedback | Roadmap page, feedback form with Resend email, rate limiting |
| 7 | Admin CMS | Admin dashboard, notes CRUD, roadmap CRUD, users view, feedback inbox |
| 8 | Polish | Loading states, error pages, SEO, security testing checklist |
| 9 | Launch | Final testing, deploy to production, soft launch to 10 users |

**Buffer:** Week 9 includes a 3-day buffer for bugs. If you finish early, you start v1.1 planning. If you finish late, you cut scope — never extend the timeline.

---

## 10. Week 1 Daily Tasks

Each day: 15 min plan, 3h 15m build, 20 min document, 10 min commit.

### Day 1 — Repo + Next.js

- Rename branch: `git branch -m master main`
- Run: `npx create-next-app@latest . --typescript --tailwind --app --no-src-dir` (choose No for src dir)
- Actually choose **yes** for src dir — it makes imports cleaner
- Test: `npm run dev` — see the default page at localhost:3000
- Create GitHub repo `keetbox` (lowercase)
- Push: `git remote add origin ...` then `git push -u origin main`
- Connect Vercel to the repo, deploy
- **Deliverable:** Live default Next.js page on Vercel

### Day 2 — Layout Shell

- Create `src/components/nav.tsx` and `src/components/footer.tsx`
- Update `src/app/layout.tsx` to include nav + footer
- Add basic typography and color tokens to `globals.css`
- **Deliverable:** Every page shows nav and footer

### Day 3 — Docs Folder

- Create `docs/00-master-plan.md` (copy this file)
- Create `docs/01-daily-log.md` (template)
- Create `docs/02-backlog.md` (list of v1.1 features)
- Create `docs/03-decisions.md` (why each stack choice was made)
- **Deliverable:** Documentation structure committed

### Day 4 — Homepage

- Build `src/app/page.tsx` with hero, pitch, featured notes placeholder
- No real notes yet — hardcode 3 placeholder cards
- **Deliverable:** Homepage looks like a real product

### Day 5 — Static Pages

- Build `src/app/terms/page.tsx`
- Build `src/app/privacy/page.tsx`
- Build `src/app/about/page.tsx`
- **Deliverable:** Three static pages done

### Day 6 — Polish + Review

- Review the week's code
- Fix any bugs
- Write `docs/weekly/W01.md` — what shipped, what was hard, what's next
- **Deliverable:** Weekly summary committed

### Day 7 — Rest

No code. Review the plan for Week 2. Confirm you're still on track.

---

## 11. Daily Workflow

### The 4-Hour Block

| Block | Time | What |
|-------|------|------|
| Plan | 15 min | Open `docs/01-daily-log.md`. Write today's ONE task. Confirm nothing else is in the day. |
| Build | 3h 15m | One task. No extra tabs. If stuck 20 min, ask AI. If stuck 45 min, break the task smaller. |
| Document | 20 min | Write what you did in `docs/01-daily-log.md`. What worked, what broke, what you learned. |
| Commit | 10 min | `git add . && git commit -m "feat: [what you did]" && git push` |

### Weekly (Sunday, 1 hour)

- Read the week's daily logs
- Update `docs/02-backlog.md`
- Write `docs/weekly/YYYY-WW.md` — what shipped, what's blocked, what's next

### Rules

1. **One task per day.** Not two. Not "while I'm here, let me also..." One.
2. **No new tools mid-week.** If you want to add a tool, add it to the backlog and revisit on Sunday.
3. **Commit every day.** Even if the commit is "WIP: stuck on X." The streak matters more than the content.
4. **No skipped days.** If you miss a day, you do not make it up. You just resume. Missing one day is fine. Missing two is a pattern.

---

## 12. Appendix

### 12.1 Glossary

- **RLS (Row Level Security):** Supabase's per-row access control. Every table needs it.
- **OTP (One-Time Password):** A 6-digit code sent to email, used once, expires in 10 minutes.
- **OAuth:** A way to sign in using another service (Google, GitHub) without creating a password.
- **JWT (JSON Web Token):** A signed token that proves who you are. Supabase uses these for sessions.
- **SPA (Single Page Application):** A web app where navigation doesn't reload the page.
- **TanStack Query:** A library that keeps data in sync between server and browser automatically.
- **shadcn/ui:** A collection of copy-paste UI components built on Radix + Tailwind. You own the code after copying.
- **Zod:** A TypeScript library for validating data shapes.
- **Middleware:** Code that runs between a request and a response — used for auth checks in Next.js.

### 12.2 References

- Next.js Docs: https://nextjs.org/docs
- Supabase Docs: https://supabase.com/docs
- Tailwind CSS: https://tailwindcss.com/docs
- shadcn/ui: https://ui.shadcn.com
- TanStack Query: https://tanstack.com/query
- Resend: https://resend.com/docs
- Vercel: https://vercel.com/docs

### 12.3 v1.1 Detailed Plan (placeholder)

To be written after v1 launches and you have real user feedback.

### 12.4 v2 Detailed Plan (placeholder)

To be written 3 months after v1.1 ships.

### 12.5 Decision Log

Every significant decision gets one line here with a date and reason.

- **2026-10-10:** Stack locked — Next.js 15 + TypeScript + Tailwind + Supabase + Vercel + Resend. Reason: all free tier, all industry-standard, all documented well.
- **2026-10-10:** v1 scope cut to admin-only accounts and feedback form. Reason: 4-hour daily budget cannot support community features in 9 weeks.
- **2026-10-10:** Business model revised to freemium. Reason: honest about future monetization; v1 stays free.
- **2026-10-10:** Repo name: `keetbox` (lowercase). Reason: convention. Caps look amateur in terminal output.
