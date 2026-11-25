# ScamSafe security checklist

Done in the site code
- Content-Security-Policy (meta tag + `_headers`): only your own files, jsDelivr (Supabase library), Google Fonts, your Supabase project, OpenAI (optional chatbot) and privacy-friendly YouTube are allowed. Plugins and base-tag tricks are blocked.
- Referrer policy, no phone-number auto-linking.
- Client-side login lockout after 5 wrong passwords (slows guessing; not a substitute for server limits).
- All user-supplied text is already escaped before display; gift notes are fixed text.

Do these in Supabase / hosting (a browser page cannot enforce them)
1. Row Level Security ON for every table and storage bucket; test with a second account.
2. Auth > Attack Protection: enable CAPTCHA (Turnstile/hCaptcha), leaked-password protection, and a minimum password length of 10+.
3. Auth > Rate limits: keep email/OTP/sign-in limits low.
4. Never put the service_role key in this page (only the publishable key is there now).
5. Host with HTTPS and apply `_headers` (Netlify / Cloudflare Pages). On other hosts copy these headers into the server config. Add `frame-ancestors 'none'` (already in `_headers`; it cannot be set from a meta tag).
6. Turn on MFA/passkeys for the Supabase and hosting admin accounts.
7. XP is stored in the browser and synced, so a determined user can edit it. Treat XP as for fun, never for anything of value. For real protection, award XP in a Supabase function.
