# Emoji Library Redirects

Netlify site that redirects old CEP extension URLs to the current Cloudflare Pages hosting.

Branch deploys handle the old Netlify URLs:
- `v2-aescripts--emojilibrary.netlify.app` → `v2-aescripts.emojilibrary.jamesxdigital.com`
- `v2--emojilibrary.netlify.app` → `v2.emojilibrary.jamesxdigital.com`

Those two branch deploys expire on the free plan and take their hostnames with them. A
weekly timer on `jamesxserver` rebuilds them and Cronitor alerts if either stops
answering 301. See `CLAUDE.md`.
