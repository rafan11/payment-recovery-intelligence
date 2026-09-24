# Payment Recovery Intelligence

A minimal SaaS MVP for invoice payment-risk monitoring and cash-flow visibility.

## Stack
- Next.js + React + TypeScript
- Tailwind CSS
- Supabase-ready schema/auth structure
- Recharts-ready dependency for future chart upgrades
- Demo mode works without Supabase

## Run
```bash
npm install
npm run dev
```
Open http://localhost:3000.

## Supabase
Copy `.env.example` to `.env.local`, add your project URL and anon key, then run `supabase/schema.sql` in the Supabase SQL editor. The current UI intentionally falls back to fictional demo data when env vars are absent.

## Risk engine
`lib/demo.ts` contains the transparent rule-based engine. Inputs include prior late payments, average days late, due-date proximity, overdue status, unpaid invoices, and amount. Scores map to Low 0–29, Medium 30–59, High 60–100. The engine is isolated so a future ML service can replace it without redesigning the UI.

## Production notes
Before public deployment, add Supabase Auth, row-level security policies, server-side invoice mutations, audit logging, rate limiting, validation (e.g. Zod), and a real AI provider only if needed for message generation. Never expose a service-role key to the browser.
