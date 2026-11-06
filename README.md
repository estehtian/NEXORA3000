# NEXORA 3000 — International Digital Platform

Starter full-stack foundation built with Next.js App Router, Supabase, Vercel, Cloudflare and GitHub.

> This is a development starter, not a fully finished enterprise marketplace. Admin authorization, production RLS policies, email templates, payment processing, legal pages, monitoring and backup operations must be completed and tested before public commercial launch.

## 1. Requirements

- Node.js 22 LTS (or a currently supported compatible LTS release)
- npm
- Git
- GitHub account
- Supabase account
- Vercel account

## 2. Run locally (Windows)

1. Extract the ZIP.
2. Open the extracted `nexora-international-platform` folder.
3. Open PowerShell in that folder.
4. Run:

```powershell
npm install
Copy-Item .env.example .env.local
```

5. Open `.env.local` and fill in the Supabase Project URL and publishable key.
6. Start the development server:

```powershell
npm run dev
```

7. Open http://localhost:3000.

## 3. Create Supabase project

1. Create a new Supabase project.
2. Open Project Settings / API (or API Keys in the current dashboard).
3. Copy the Project URL and publishable key.
4. Put them in `.env.local`:

```env
NEXT_PUBLIC_SUPABASE_URL=https://YOUR_PROJECT_REF.supabase.co
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=YOUR_PUBLISHABLE_KEY
```

5. In Supabase SQL Editor, run `supabase/migrations/0001_initial_schema.sql`.
6. In Authentication settings, enable the sign-in methods you intend to support and configure the Site URL and redirect URLs.
7. Test registration and login.

Never put a Supabase secret/service-role key in browser code, GitHub, or any `NEXT_PUBLIC_` variable.

## 4. Push to GitHub

Create an empty repository named `nexora-international-platform`, then run:

```bash
git init
git add .
git commit -m "Initial NEXORA platform"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/nexora-international-platform.git
git push -u origin main
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

## 5. Deploy to Vercel

1. Sign in to Vercel with GitHub.
2. Select Add New → Project.
3. Import `nexora-international-platform`.
4. Add the two Supabase environment variables from `.env.local` in Project Settings → Environment Variables.
5. Deploy.
6. Test the generated Vercel URL.

Vercel Hobby is intended for personal, non-commercial use. Review the current Vercel plan terms before operating a commercial platform; upgrade or choose a host whose terms fit your use.

## 6. Cloudflare and custom domain

Do not change nameservers or DNS records until you have a domain and have inspected its current DNS.

1. Add the domain to Cloudflare.
2. Review and preserve required MX, TXT, verification and existing service records.
3. If moving authoritative DNS to Cloudflare, use only the nameservers Cloudflare assigns for that domain.
4. Add the domain in Vercel → Project Settings → Domains.
5. Follow the exact DNS values Vercel displays.
6. Wait for DNS verification and TLS certificate issuance.
7. Test HTTPS and both apex/www hostnames.

Do not guess IP addresses or nameservers. Avoid enabling proxying for records until the Vercel DNS and TLS setup is verified.

## 7. Included routes

- `/` — public landing page
- `/about` — about
- `/services` — capabilities
- `/pricing` — planning tiers (not live billing)
- `/contact` — contact placeholder
- `/register` — Supabase email registration
- `/login` — Supabase email login
- `/dashboard` — authenticated user page
- `/admin` — deliberately unprivileged placeholder
- `/api/health` — basic health endpoint

## 8. Important security work before production

- Implement server-side admin and partner authorization; the `/admin` page is not protected admin functionality.
- Add role provisioning through a trusted server-side process. Never let a user assign themselves `admin`.
- Complete and test RLS policies for every table and Storage bucket.
- Add email confirmation, password recovery, MFA for privileged users and session handling.
- Add rate limiting, bot protection, CSRF protections appropriate to each mutation, input validation and upload restrictions.
- Add audit logging for privileged operations.
- Configure backups and perform a restore test.
- Add privacy policy, terms, cookie notice and data-retention process for relevant jurisdictions.
- Add monitoring, error reporting, dependency/security scanning and incident response.
- Review accessibility, performance, SEO, localization and legal requirements.

## 9. Commands

```bash
npm run dev
npm run typecheck
npm run lint
npm run build
npm start
```

## 10. Suggested next implementation sequence

1. Complete middleware/session refresh if needed for the chosen Supabase SSR setup.
2. Build secure server-side role checks and protected admin routes.
3. Add partner organization membership workflows.
4. Add products/content CRUD with approval states and strict RLS.
5. Add Storage buckets with upload policies.
6. Add notifications and audit events.
7. Add tests for authorization boundaries and database policies.
8. Add payment provider only after business, legal and compliance requirements are defined.
