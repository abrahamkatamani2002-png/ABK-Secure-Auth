# ABK — HTML/CSS/JavaScript + Supabase
No PHP, Laragon, local MySQL or local backend required. Supabase provides managed Auth and online PostgreSQL.

## Setup
1. Create a project at https://supabase.com/.
2. Run `supabase/schema.sql` in Supabase SQL Editor.
3. In Authentication settings enable Email provider, email confirmation and email OTP; configure custom SMTP for reliable delivery.
4. Copy your project URL and public anon/publishable key from Project Settings → API into `config.js`.
5. Never put the `service_role` key, database password, SMTP password or AWS secrets in this folder.
6. Set Supabase Auth Site URL and Redirect URLs to your deployed site URL.
7. Deploy this folder to Netlify (publish directory is `.`) or another static host with HTTPS. For local testing use VS Code Live Server.

## First administrator
Every new account is assigned `user`. Register your own account, find its UUID in Supabase Authentication → Users, then run this trusted one-time SQL after checking the identity:
`UPDATE public.profiles SET role='super_admin' WHERE id='YOUR_AUTH_USER_UUID';`
Never add role selection to the public signup form.

## Security architecture
- Supabase Auth handles password hashing, credentials, session tokens and email OTP.
- PostgreSQL RLS and column-level grants enforce access on the database.
- Browser config contains only the public anon/publishable key. A public key is safe only when RLS is correctly configured.
- Admin role changes, archival/deletion, trusted audit insertion, backup/restore and AWS actions are intentionally not implemented in browser code. Add reviewed Supabase Edge Functions for these privileged actions.
- Email OTP is a useful second step but not phishing-resistant MFA. Enable Supabase TOTP MFA and require it for administrators for stronger protection.
- Use Supabase managed backups/PITR and test restoration separately. Do not attempt full database restore from a browser application.

## Notes
The included starter is not yet production-certified. Configure SMTP, email confirmation, password rules, Auth rate limits/CAPTCHA, MFA, RLS and backups, then test with separate normal/admin accounts. `docs/TEST_PLAN.md` provides a test checklist.
