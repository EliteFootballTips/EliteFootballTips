ELITE FOOTBALL TIPS V2 — LIVE FIXTURES + ADMIN-ONLY PUBLISHING

WHAT IS INCLUDED
- Responsive installable website/PWA (Android home-screen install).
- Fixtures page powered by a Supabase Edge Function proxy to football-data.org.
- Five-minute refresh while the page is open.
- Admin sign-in using Supabase Auth.
- Predictions stored in Supabase; row-level security allows only approved admin accounts to insert/update/delete.
- Public visitors can read published predictions only.

IMPORTANT LIMITATIONS
- Live fixture data is NOT active until you create/configure Supabase and obtain a football-data.org API token.
- Provider coverage, competition availability, update frequency and live status depend on the provider's plan and data.
- This is a PWA, not a Play Store APK.
- Do not publish any demo or unverified picks as real tips.
- This is an information/prediction website, not a betting operator. Do not collect stakes or accept wagers.

SETUP (free tiers may be sufficient; check provider limits/pricing)
1. Create a Supabase project at https://supabase.com.
2. In Supabase SQL Editor, run supabase/schema.sql.
3. In Supabase Authentication > Users, create your own admin user with email/password.
4. Copy that user's UUID. In SQL Editor run:
   insert into public.admin_users(user_id) values ('YOUR-AUTH-USER-UUID');
   This is the admin allow-list. Never expose a service_role key.
5. Install Supabase CLI and link your project:
   supabase login
   supabase link --project-ref YOUR_PROJECT_REF
6. Set the football-data.org API token as a server secret:
   supabase secrets set FOOTBALL_DATA_TOKEN=YOUR_PROVIDER_TOKEN
7. Deploy the fixture proxy:
   supabase functions deploy fixtures
8. In config.js, replace YOUR_PROJECT and YOUR_SUPABASE_ANON_KEY with your Supabase project URL and anon/public key. Never paste service_role key.
9. Upload the website files (index.html, config.js, manifest.json, sw.js, icon.svg) to a public GitHub repository.
10. Enable GitHub Pages: repository Settings > Pages > Deploy from a branch > main > /(root).
11. Open the published HTTPS URL. The fixtures page refreshes every five minutes while open.
12. For Android: open the site in Chrome > menu > Install app or Add to Home screen.

SUPPORTED COMPETITION CODES IN THIS STARTER
PL = Premier League; PD = La Liga; BL1 = Bundesliga; SA = Serie A; FL1 = Ligue 1.
“All competitions” requests the provider's general matches endpoint. Availability depends on your provider plan.

ADMIN SECURITY
- Supabase Auth handles passwords; this app does not store passwords itself.
- Admin publishing is enforced by database RLS policies, not just by hiding buttons.
- Only add your own trusted auth user UUID to admin_users.
- Do not share your admin login.
- For production, add rate limits, stronger audit logging, privacy/terms pages, and test RLS policies.

UGANDA
Before adding wager collection, bookmaker odds-taking, deposits, payouts or any betting operation, consult Uganda's National Lotteries and Gaming Regulatory Board and qualified local counsel. This starter intentionally does not handle bets or customer money.
