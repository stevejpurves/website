# Deploying euclidity.com

End-to-end checklist for taking this repo from your laptop to live at `https://euclidity.com`. Roughly 30 minutes of work, plus DNS propagation and GitHub Pages cert provisioning (each ~10 min in the worst case).

You'll do four things, in order:

1. **Form backend** — wire up Formspree so the contact form actually sends email
2. **Git + GitHub** — create the repo and push
3. **GitHub Pages** — enable Pages and bind the custom domain
4. **DNS** — point `euclidity.com` at GitHub's edge

Then a smoke test.

---

## 0. Pre-flight

From the project root, confirm a clean production build:

```bash
npm run build
```

Should finish with `4 page(s) built` and no errors. If anything fails, fix it before going further — you do not want to debug Tailwind classes against the live site.

---

## 1. Form backend (Formspree)

The contact form on `/about` posts to `https://formspree.io/f/REPLACE_WITH_YOUR_FORM_ID` ([src/pages/about.astro](src/pages/about.astro), one occurrence). Until you replace that placeholder, submissions 404.

### 1a. Create the form

1. Go to [formspree.io](https://formspree.io) and sign up with `ops@euclidity.com` (or whichever address should receive submissions).
2. **+ New project** → name it `euclidity-website`.
3. Inside the project: **+ New form** → name it `Contact` → **Create form**.
4. Copy the endpoint shown — looks like `https://formspree.io/f/xanybkdq`. The trailing 8-char id is what you need.
5. **Verify your email**: Formspree emails the address you signed up with. Click the link. Until you do, submissions are silently dropped.

### 1b. Wire it into the site

Edit [src/pages/about.astro](src/pages/about.astro), locate the `<form>` tag, and replace the placeholder:

```astro
<form
  class="space-y-12"
  action="https://formspree.io/f/xanybkdq"   {/* ← your real id */}
  method="POST"
>
```

### 1c. Recommended hardening (10 min, optional)

Inside the same `<form>`, add these three hidden inputs before the submit button:

```astro
<input type="text" name="_gotcha" tabindex="-1" autocomplete="off" class="hidden" />
<input type="hidden" name="_subject" value="New consultation request — euclidity.com" />
<input type="hidden" name="_next" value="https://euclidity.com/about?sent=1" />
```

- `_gotcha` is a honeypot — bots fill it, humans don't see it, anything posted with a value is dropped.
- `_subject` makes inbox triage saner.
- `_next` redirects the visitor back to your site after submit instead of Formspree's default thank-you page.

You can later add a `?sent=1` confirmation banner on `/about` — out of scope for first deploy.

### 1d. Free-tier limits

Formspree free is **50 submissions/month** with basic spam filtering. Plenty for a consultancy contact form. If volume grows, upgrade or swap to Basin / Web3Forms (drop-in compatible — same form-POST contract, just change the URL).

---

## 2. Git + GitHub

This repo isn't a git repo yet. Initialize, commit, and push.

### 2a. Initialize the repo locally

```bash
cd /Users/stevejpurves/dev/eu/website
git init
git add .
git commit -m "Initial commit — Euclidity SL website"
```

The `.gitignore` already excludes `node_modules/`, `dist/`, `.astro/`, `.DS_Store`, and `.env*`.

### 2b. Create the GitHub repo

If you have the GitHub CLI:

```bash
gh repo create euclidity/website --public --source=. --remote=origin --push
```

(Replace `euclidity` with the org or user that should own it.)

If not, create the repo manually on github.com (do **not** initialize with a README), then:

```bash
git remote add origin git@github.com:<owner>/<repo>.git
git branch -M main
git push -u origin main
```

The push triggers `.github/workflows/deploy.yml`, which builds and uploads `dist/` as a Pages artifact. The first run will fail to deploy until step 3 — that's expected.

---

## 3. GitHub Pages

In your repo on github.com:

1. **Settings → Pages**
2. **Build and deployment → Source**: choose **GitHub Actions** (not "Deploy from a branch")
3. **Custom domain**: enter `euclidity.com` → **Save**
   - GitHub will run a DNS check; it'll fail until step 4 — that's fine, leave it.
4. Leave **Enforce HTTPS** unticked for now. You'll enable it after the cert provisions.

The `public/CNAME` file (already in the repo, contents `euclidity.com`) gets copied into `dist/` on every build, so the custom-domain binding survives every deploy. Don't delete it.

---

## 4. DNS

At your domain registrar (wherever `euclidity.com` is registered), point the apex and `www` at GitHub Pages.

### 4a. Apex (`euclidity.com`) — four A records

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

### 4b. `www` subdomain (recommended) — one CNAME

| Type | Name | Value |
|---|---|---|
| CNAME | www | `<owner>.github.io.` |

Replace `<owner>` with your GitHub user/org (the same one in the repo URL). The trailing `.` is fine to include if your registrar accepts it.

### 4c. TTL

Set TTL to 300–600s for the first switch — if anything's wrong you can fix it fast. Bump to 3600s once you're happy.

### 4d. Propagation

Run:

```bash
dig +short euclidity.com
dig +short www.euclidity.com
```

Should show the four GitHub IPs and your `<owner>.github.io` respectively, within 5–15 minutes for most registrars (slower for some — Cloudflare is fast, GoDaddy can be 30+ min).

### 4e. Back to GitHub Pages → Settings → Pages

Once `dig` looks right:

1. The DNS-check banner clears automatically.
2. GitHub provisions a Let's Encrypt cert — usually 5–10 min, occasionally up to 24h.
3. When the cert is ready, **Enforce HTTPS** is no longer greyed out — tick it.

---

## 5. Smoke test

```bash
curl -I https://euclidity.com/
curl -I https://euclidity.com/services
curl -I https://euclidity.com/projects
curl -I https://euclidity.com/about
```

All four should return `HTTP/2 200`. Then in a browser:

- [ ] All four pages load and look right
- [ ] Nav active state is correct on each page
- [ ] Hero images load (no broken-image icons — every `<img>` references `/images/*`, all locally hosted)
- [ ] Submit the contact form on `/about` with real input
- [ ] Email arrives at `ops@euclidity.com` within 30 seconds
- [ ] Reply to it once to whitelist Formspree's relay address

---

## Future deploys

Once everything's wired:

```bash
git add <files>
git commit -m "..."
git push
```

That's it. The Actions workflow builds and deploys on every push to `main`. Watch progress under **Actions** in the repo.

To trigger a manual rebuild without changing code (e.g. after rotating a secret), go to **Actions → Deploy to GitHub Pages → Run workflow**.

---

## Common gotchas

- **404 after deploy**: usually means `public/CNAME` got removed, or DNS hasn't propagated. Re-add the CNAME file with `euclidity.com` (no trailing newline issues — keep it as-is).
- **Form posts but no email**: did you verify the email at Formspree? Check your spam folder for the verification mail. Until that's done, every submission is silently dropped.
- **Cert stuck "in progress" for >24h**: remove and re-add the custom domain in Pages settings — usually unsticks it. Make sure all four A records are correct and there's no AAAA record overriding them.
- **Workflow runs but Pages stays on old version**: check that **Settings → Pages → Source** is set to **GitHub Actions**, not "Deploy from a branch."
- **Mixed-content warnings**: shouldn't happen — the site has no external assets after the image-pull (all `/images/*` are local). If they do, search for `http://` in `src/`.

---

## Files referenced

- [.github/workflows/deploy.yml](.github/workflows/deploy.yml) — build & publish action
- [public/CNAME](public/CNAME) — custom domain binding (`euclidity.com`)
- [astro.config.mjs](astro.config.mjs) — `site: 'https://euclidity.com'` (used for canonical URLs in `<head>`)
- [src/pages/about.astro](src/pages/about.astro) — contact form, contains the `REPLACE_WITH_YOUR_FORM_ID` placeholder
