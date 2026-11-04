# Arshem LegalCore — sales site

A single-page, self-contained sales/marketing landing page for Arshem LegalCore.
No backend, no build step, no dependencies beyond two Google Fonts — it's one
`index.html` with inline CSS and JS.

## What's on the page

- A live-animated AI redline demo, a network-isolated upload sandbox flow,
  and an auto-scrolling audit-log ticker, all grounded in Arshem's actual
  product surface (not placeholder copy).
- A real, working `⌘K` command palette (press it anywhere on the page) that
  jumps to any section, toggles light/dark theme, or opens the demo-request form.
- A FAQ section (`#preguntas`) answering the objections a legal buyer actually
  has — audience fit, AI-edit visibility, encryption, the upload sandbox,
  per-document permissions, verifiable deletion, pricing/onboarding — as a
  native `<details>` accordion (no JS, fully keyboard- and screen-reader-
  accessible). Every answer is grounded in what the product actually does;
  nothing here is a placeholder.
- A "Solicitar una demo" modal wired to **Netlify Forms** (name/email/firm/
  interest, plus a honeypot field for spam). Submitting it only works as a
  real form once this site is actually deployed on Netlify — see below. On
  every other host (including this file previewed locally or via an
  Artifact) it falls back automatically to opening a `mailto:` to
  `arshem.tech@gmail.com` with the same details pre-filled, so the form
  never silently fails.
- Full light/dark theming (follows system preference, with a manual toggle),
  responsive layout, and `prefers-reduced-motion` support throughout.

## Local preview

No build step — just open the file:

```bash
open index.html
```

or serve it (recommended, since some browsers restrict `file://` fetches):

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deploying

This is a static site — it doesn't need a server, and specifically doesn't
need to live on the product's EC2 box. Any static host works with **zero
configuration** (no build command, no output directory to set, just point it
at this repo):

- **Vercel** — [vercel.com/new](https://vercel.com/new), import this repo, deploy. Done.
- **Netlify** — [app.netlify.com/start](https://app.netlify.com/start), same flow.
- **Cloudflare Pages** — same flow, via the Cloudflare dashboard.
- **GitHub Pages** — Settings → Pages → Deploy from branch → `main` / `/ (root)`.

All four give you free hosting, a CDN, and automatic HTTPS, and redeploy
automatically on every push to `main`.

**If you deploy to Netlify**, the demo-request form works out of the box —
no extra setup. Netlify detects the `data-netlify="true"` form in the static
HTML at deploy time and starts collecting submissions under **Forms** in the
site dashboard, where you can also turn on an email notification per
submission. On any other host, the form still works, just via the `mailto:`
fallback described above.

## Updating the lead-capture flow

`demoForm`'s submit handler (in `index.html`) tries a Netlify Forms POST
first and falls back to `mailto:` if that fails — see the comments around
`isArtifactPreview` and `sendViaMailtoFallback`. If you move off Netlify
and want a different backend (Formspree, Getform, the product's own API),
replace the `fetch("/", ...)` call with that provider's endpoint; the form
fields and validation don't need to change.
