# ScamSafe

ScamSafe is an interactive learning site for cybersecurity, scam awareness, AI literacy, and cloud safety. It includes a phishing inbox simulator, decision-based scenarios, browser/device read-aloud controls, a voice-cloning safety exercise, and official CISA alert headlines.

## Run locally

Requirements: Node.js `>=22.12.0` and npm.

```powershell
npm install
npm run dev
```

Open the local URL printed by Vite. Create a production build with:

```powershell
npm run build
```

The static production output is written to `dist/`.

## Supabase setup

Authentication, progress sync, community chats, and private feedback use Supabase. Follow [SUPABASE_SETUP.md](./SUPABASE_SETUP.md) and apply only the SQL sections for features you enable. The browser uses a Supabase publishable key; never put a Supabase service-role key, provider secret, or other privileged credential in browser code.

The feedback form requires the **Private site feedback** SQL section. Feedback is available to signed-in users and is private to the Supabase project administrators; it is not shown publicly.

## Privacy and external services

- The AI chatbot sends its prompts to the configured AI provider. See the in-app Privacy Policy before using it.
- Community messages and private feedback are stored in Supabase when those features are configured.
- The home page requests public CISA cybersecurity advisories through a read-only Supabase Edge Function. Deploy `scamsafe-alerts` as described in [SUPABASE_SETUP.md](./SUPABASE_SETUP.md); if the feed is unavailable, the page reports the problem and links to official agency pages.
- Read-aloud and example voice clips use browser/device speech synthesis; available voices depend on the device.

## Contributing

Read [CONTRIBUTING.md](./CONTRIBUTING.md) before opening an issue or pull request. Never include real scam victims' personal details, credentials, or live malicious links in examples.

## Publish with GitHub Pages

The GitHub Actions workflow in `.github/workflows/pages.yml` builds the Vite app and publishes `dist/` to GitHub Pages. In the repository, open **Settings → Pages** and set **Source** to **GitHub Actions**. Push the project to the `main` branch (or change the workflow trigger to match your default branch); then check the **Actions** tab for the deployment result. The published URL is shown under **Settings → Pages**.

Do not publish the source folder directly as a Pages branch: Vite must build the app first so its scripts, styles, and asset paths work on a project site such as `https://OWNER.github.io/REPOSITORY/`. Netlify is optional; you only need one hosting provider.

No custom domain is configured. If you choose one later, follow the hosting provider's domain setup instructions before adding DNS records or a `CNAME` file.

No license is included yet. Until the authors choose and add a license, public visibility alone does not grant permission to reuse, modify, or redistribute the source.
