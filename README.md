# Euclidity SL — website

Static marketing site for Euclidity SL. Built with [Astro](https://astro.build) and Tailwind v4. Deploys to GitHub Pages with the `euclidity.com` custom domain.

## Local development

```bash
npm install      # one-time
npm run dev      # http://localhost:4321 with hot-reload
npm run build    # produce dist/ for production
npm run preview  # serve the production build locally
```

## Project layout

```
src/
  layouts/Layout.astro       Global <head>, header, footer wrap
  components/
    Header.astro             Top nav, takes active={'services'|'projects'|'about'}
    Footer.astro             Site footer
    Logo.astro               <img> wrapper for /logo-mark.png
    Icon.astro               Inline SVG icons (Material Symbols paths)
  pages/
    index.astro              Home
    services.astro
    projects.astro
    about.astro              Includes #contact form section
  styles/global.css          Tailwind @theme tokens, brutalist primitives
public/
  logo-mark.png              Recolored logo (deep green)
  favicon.ico, icon-*.png    Generated from logomark
  apple-touch-icon.png
  CNAME                      euclidity.com (do not delete)
designs/                     Reference HTML and screenshots — not built
```

## Design tokens

Defined in `src/styles/global.css` inside the Tailwind v4 `@theme` block. To change a color, font size, or spacing token, edit there — every page picks it up automatically.

The two-tone green accent:

| Token | Hex | Use |
|---|---|---|
| `primary` | `#006B1F` | Text, borders, label-caps, logo |
| `primary-container` | `#00FF41` | Solid fills, badges, hover surfaces (always with `on-primary-container` = black text) |

## Editing pages

Each `.astro` page is plain HTML inside `<Layout>`. Frontmatter (between `---`) is for imports and per-page constants. Content lives directly in the markup — no CMS, no MDX (yet). Add a new page by dropping a file into `src/pages/`; the route matches the filename.

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds and publishes `dist/` to GitHub Pages.

**One-time GitHub setup:**

1. Repo → Settings → Pages → Source: **GitHub Actions**.
2. Repo → Settings → Pages → Custom domain: enter `euclidity.com` and tick **Enforce HTTPS** once the cert provisions.
3. At your DNS provider, point `euclidity.com` apex to GitHub Pages IPs:
   - A 185.199.108.153
   - A 185.199.109.153
   - A 185.199.110.153
   - A 185.199.111.153
   - (optional) `www` CNAME → `<user>.github.io`
4. The `public/CNAME` file is included in the build artifact, so the custom domain stays bound on every deploy.

## Known TODOs

- **Placeholder images.** All `<img>` tags currently load from `lh3.googleusercontent.com` (URLs from the design tool). They render today but aren't permanent — replace with real assets in `public/images/` and update each page's `src=`.
- **Contact form.** `src/pages/about.astro` posts to `https://formspree.io/f/REPLACE_WITH_YOUR_FORM_ID`. Sign up at formspree.io (or swap to another no-backend handler — Basin, Web3Forms, Netlify Forms if migrating) and replace the form ID.
- **Logo refinement.** `public/logo-mark.png` is the design's red mark recolored to deep green. For perfect crispness at all sizes, an SVG version would be better than the 600×600 PNG.
