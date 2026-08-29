# CLAUDE.md - Emoji Library Redirects

Netlify redirect site for old Emoji Library CEP extension installs that still point to Netlify URLs.

## How It Works

Old ZXP builds (v2.0.1 and earlier) hardcoded Netlify branch deploy URLs. This site redirects them to the current Cloudflare Pages hosting.

- `v2-aescripts--emojilibrary.netlify.app` → `v2-aescripts.emojilibrary.jamesxdigital.com`
- `v2--emojilibrary.netlify.app` → `v2.emojilibrary.jamesxdigital.com`

## Deployment

Netlify site `emojilibrary`, connected to this repo on GitHub. No build command; the
repo root is published as-is. Branch deploys are enabled for `main`, `v2` and
`v2-aescripts`. `main` is production and answers both `emojilibrary.netlify.app` and
`main--emojilibrary.netlify.app`.

**Branch deploys expire.** The free plan keeps only the published production deploy, and
a `<branch>--<site>.netlify.app` hostname points at one specific deploy. Once the `v2`
and `v2-aescripts` deploys are pruned their hostnames return a bare Netlify 404 and every
pre-2.0.2 panel is dead. Nothing recreates them but a new build of that branch. This is
not fixable from `main`: hostname resolution happens before any `_redirects` rule runs.

It failed exactly this way between 2026-05-05 and 2026-08-28, and a customer reported it
rather than any alarm. Two guards on `jamesxserver` now cover it:

- `emojilibrary-redirect-refresh.timer` rebuilds both branches every Monday through the
  Netlify build hooks in `/etc/emoji-library/netlify-hooks.env`.
- Cronitor checks `emojilibrary-redirect-v2` and `emojilibrary-redirect-v2-aescripts`
  assert a 301 every 30 minutes.

## Do NOT delete this site — users with old CEP installs depend on these redirects.

## Related

- Main repo: `jamesxdigital/emoji-library`
- Cloudflare Pages projects: `emojilibrary-gumroad`, `emojilibrary-aescripts`
