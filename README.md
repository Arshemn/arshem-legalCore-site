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
- A "Solicitar una demo" modal that composes a `mailto:` to `ventas@arshem.ai`
  with the visitor's name/email/firm/interest — there's no form backend yet,
  so this is the delivery mechanism until one exists (see below).
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

## Updating the lead-capture flow

The demo-request form currently sends through the visitor's own email client
via a `mailto:` link (see the `demoForm` submit handler in `index.html`).
Once there's a real form backend (e.g. Formspree, Getform, or the product's
own API), swap that handler to a `fetch()` POST instead — the form fields
and validation don't need to change.
