# CLAUDE.md — Optimist PCs Website

This file provides context for Claude across sessions. Update it as the project progresses.

---

## Project Overview

Official website for **Optimist PCs** (`optimist.gg`) — a luxury custom PC company. This is a full ground-up redesign and rebuild, not a migration of the old site.

---

## Current Status

### Completed
- Project scaffolded with SvelteKit 2 (Svelte 5, minimal template)
- TypeScript enabled
- Tailwind CSS v4 + typography plugin installed
- Prettier + ESLint configured
- Vercel adapter installed
- shadcn-svelte initialized
- All core packages installed (see stack below)
- `.gitignore` configured (added `.vercel` entry)
- `README.md` created
- `CLAUDE.md` created (this file)

### Not Yet Done
- `.env` file not created — no API keys configured yet
- Supabase project not connected
- Stripe keys not added
- Cloudinary account not connected
- Resend not configured
- Klaviyo not set up
- GA4 script tag not added to `app.html`
- No pages or components built yet
- No routes created yet

---

## Tech Stack

| Layer | Tool | Status |
|---|---|---|
| Framework | SvelteKit 2 + Svelte 5 |  Installed |
| Language | TypeScript |  Installed |
| Styling | Tailwind CSS v4 + typography plugin |  Installed |
| Linting/Formatting | ESLint + Prettier |  Installed |
| Components | shadcn-svelte |  Installed |
| Animation | GSAP + ScrollTrigger + Lenis |  Installed (ScrollTrigger TBD) |
| Images | svelte-cloudinary |  Installed |
| Database | Supabase (RLS) |  Installed · Not connected |
| Auth | Supabase Auth |  Installed · Not connected |
| Payments | Stripe |  Not Installed · No keys |
| Email (transactional) | Resend |  Installed · No keys |
| Email (marketing) | Klaviyo | Script tag only — add closer to launch |
| Shipping | Shippo API | REST API — no install needed |
| Analytics | Supabase custom + GA4 | GA4 script tag — add closer to launch |
| Admin tables | TanStack Table | Deferred to admin dashboard phase |
| Package Manager | npm |  |
| Hosting | Vercel |  Adapter installed · Not deployed yet |

---

## Environment Variables Needed

These need to be added to `.env` before any backend work can begin. Create `.env` from `.env.example`.

```bash
# Supabase
PUBLIC_SUPABASE_URL=
PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Stripe
PUBLIC_STRIPE_PUBLISHABLE_KEY=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

# Resend
RESEND_API_KEY=

# Cloudinary
PUBLIC_CLOUDINARY_CLOUD_NAME=

# Shippo
SHIPPO_API_KEY=
```

## Architecture Notes

- **OOP configurator:** Each PC model will be a class extending a base abstract class. This is the most complex feature — intersection of OOP architecture, pricing logic, UI, and Stripe integration. Deferred to later phase.
- **Supabase RLS:** Row Level Security is the steepest learning curve in the stack. Take care when setting up policies.
- **GSAP init:** ScrollTrigger should be registered once in the root layout, not per-component.
- **Lenis:** Initialize globally. Always wrap animations in `prefers-reduced-motion` checks.
- **Svelte 5 runes:** Use `$state`, `$derived`, `$effect` — not the old Svelte 4 reactive syntax.
- **shadcn-svelte components:** Add individually with `npx shadcn-svelte@latest add [component]`
- **Supabase types:** After schema changes run `npx supabase gen types typescript --project-id YOUR_ID > src/lib/types/database.types.ts`

---

## Planned Project Structure

```
src/
├── lib/
│   ├── components/       # Shared UI components
│   ├── server/           # Server-only (Supabase admin, Stripe, Resend)
│   ├── stores/           # Svelte stores
│   ├── types/            # TypeScript types + Supabase generated types
│   └── utils/            # Helper functions
├── routes/
│   ├── (public)/         # Public-facing pages
│   ├── (admin)/          # Admin dashboard (protected)
│   └── api/              # API endpoints
└── app.html              # Root HTML (GA4 script tag goes here)
```

---

## 11-Phase Engineering Plan


| Phase | Name | Status |
|---|---|---|
| 1 | Codebase Audit |  N/A — building from scratch |
| 2 | Requirements & Scope |  Complete |
| 3 | Architecture & UML | Not started |
| 4 | Design System | Not started |
| 5 | Infrastructure & Tooling | In progress (scaffolding done, env vars pending) |
| 6 | Database & Backend | Not started |
| 7 | Frontend Core Components |  Not started |
| 8 | Frontend Public Pages | Not started |
| 9 | Admin Dashboard | Not started |
| 10 | Testing & QA | Not started |
| 11 | Launch & Migration | Not started |

---

## Next Steps

1. Create `.env` file and add all API keys
2. Connect Supabase — verify connection in a test route
3. Set up Stripe — verify webhook locally with Stripe CLI
4. Begin Phase 3 — Architecture & UML
5. Begin Phase 4 — Design system (typography, color tokens, spacing)

---

*Last updated: March 27, 2026*
