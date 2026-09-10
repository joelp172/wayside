# Wayside site

The public pages App Review requires: a one-page site, the privacy policy and a support page.
Static HTML and one stylesheet, no build step.

```
index.html        the app page
privacy/          the privacy policy, linked from About and from App Store Connect
support/          the support page, linked from About
style.css         shared, light and dark
icon.png          the app icon at 256px
```

## Publishing

The app's own repository is private, so these pages live in a **separate public repository** —
GitHub Pages only serves from a public repository on a free plan. Copy this directory into it,
then Settings → Pages → Deploy from a branch → `main` → `/ (root)`.

The URLs the app expects are in `Wayside/App/AppLinks.swift`. They currently point at
`joelp172.github.io/wayside`, which is the default Pages host for a repository named
`wayside`. Change the repository name and you must change those two constants with it.

## Custom domain

Add the domain under Settings → Pages, which writes a `CNAME` file here, then point DNS at GitHub:

- **Apex** (`wayside.app`): four A records to `185.199.108.153`, `185.199.109.153`,
  `185.199.110.153` and `185.199.111.153`, plus the matching AAAA records. Confirm these against
  GitHub's current documentation before relying on them.
- **Subdomain** (`www.wayside.app`): one CNAME to `joelp172.github.io`.

Wait for the certificate, then tick Enforce HTTPS. Finally update `AppLinks` to the new host and
paste the privacy URL into App Store Connect.

## Keeping the policy honest

This is the only copy of the privacy policy; the markdown that used to sit in `docs/` is gone, so
there is nothing to drift out of step. When the app gains anything that touches data — a new
permission, a new thing shown on the Lock Screen, a new export — change `privacy/index.html`, the
Data Privacy page in the app, and the date at the top of both.
