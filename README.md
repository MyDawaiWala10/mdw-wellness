# MDW Wellness — Public Site

**Your Wellness, Our Focus.**

The public-facing website for **MyDawaiWala (MDW) Wellness** — supportive
rehabilitation services covering **online consultations**, **home therapy**, and
comprehensive **vitals checks**. Patients discover services, book enquiries, and
returning users sign in, all from here.

> **Live:** _Coming soon — link will be added once the production domain is live._

---

## What this repo is

This is **one of three systems** that make up the MyDawaiWala product (the public
site, the back-office dashboard, and the Wellness Backend API). It is **not** a
monorepo. For the full picture of how the systems fit together and where data
lives, read [`ARCHITECTURE.md`](./ARCHITECTURE.md); for cross-repo integration
details see [`BACKEND_INTEGRATION.md`](./BACKEND_INTEGRATION.md).

In short, this site:

- **Reads** from its own **Supabase** database (auth + bookings storage).
- **Writes** booking enquiries to the **Wellness Backend** (Express + MongoDB),
  so every submission appears on the back-office dashboard automatically.

## Tech stack

- **Framework:** Next.js 16 (App Router) · React 19 · TypeScript
- **Styling:** Tailwind CSS v4 · shadcn / Base UI · `tw-animate-css`
- **Motion & UI:** Framer Motion · Embla Carousel · Lucide icons · Sonner (toasts)
- **Forms:** React Hook Form · Zod validation
- **Data / auth:** Supabase (`@supabase/ssr`, `@supabase/supabase-js`)

## Pages

| Route        | Purpose                                              |
| ------------ | --------------------------------------------------- |
| `/`          | Home — services, hero carousel, booking CTAs        |
| `/about`     | Mission, why trust us, company & location           |
| `/vitals`    | Vitals check service (checks, plans, reports, FAQ)  |
| `/grievance` | Contact & grievance redressal                       |
| `/terms`     | Terms of service                                    |
| `/privacy`   | Privacy policy                                      |
| `/auth/*`    | Authentication (Supabase callback)                  |

## Getting started

This project uses **Bun**, but `npm` / `pnpm` / `yarn` work too.

```bash
# install dependencies
bun install

# copy env template and fill in the values
cp .env.local.example .env.local

# run the dev server
bun run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the site.

## Environment variables

Copy [`.env.local.example`](./.env.local.example) to `.env.local` and set:

| Variable                          | Description                                                        |
| --------------------------------- | ----------------------------------------------------------------- |
| `NEXT_PUBLIC_SITE_URL`            | Canonical site URL — used for SEO (metadata, canonicals, sitemap) |
| `NEXT_PUBLIC_SUPABASE_URL`        | Supabase project URL (auth + bookings)                            |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY`   | Supabase anonymous/public key                                     |
| `NEXT_PUBLIC_WELLNESS_BACKEND_URL`| Wellness Backend base URL — booking enquiries POST here           |

> Variables prefixed with `NEXT_PUBLIC_` are inlined into the client bundle at
> build time.

## Scripts

| Command         | Description                  |
| --------------- | ---------------------------- |
| `bun run dev`   | Start the dev server         |
| `bun run build` | Production build             |
| `bun run start` | Serve the production build   |
| `bun run lint`  | Run ESLint                   |

## Deployment

Deployed on **Vercel**. Set the environment variables above in the Vercel project
settings before deploying.
