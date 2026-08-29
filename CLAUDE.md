# CLAUDE.md - Emoji Library Redirects

Netlify redirect site for old Emoji Library CEP extension installs that still point to Netlify URLs.

## How It Works

Old ZXP builds (v2.0.1 and earlier) hardcoded Netlify branch deploy URLs. This site redirects them to the current Cloudflare Pages hosting.

- `v2-aescripts--emojilibrary.netlify.app` → `v2-aescripts.emojilibrary.jamesxdigital.com`
- `v2--emojilibrary.netlify.app` → `v2.emojilibrary.jamesxdigital.com`

## Deployment

Netlify site `emojilibrary`, connected to this repo on GitHub. No build command; the repo
root is published as-is. Branch deploys are enabled for `main`, `v2` and `v2-aescripts`.
`main` is production and answers both `emojilibrary.netlify.app` and
`main--emojilibrary.netlify.app`.

**A branch hostname exists only while a deploy of that branch exists**, and Netlify builds a
branch only when that branch is pushed. From 2026-05-05 to 2026-08-29 no deploy of `v2` or
`v2-aescripts` existed, both hostnames served a bare Netlify 404, and every pre-2.0.2 panel
was dead. A customer reported it. Nothing here noticed.

This cannot be fixed from `main`: hostname resolution happens before any `_redirects` rule
runs, so the production deploy never sees the request.

If a hostname 404s again, push to that branch — an empty commit is enough — or use Trigger
deploy for it in Netlify. Cronitor checks `emojilibrary-redirect-v2` and
`emojilibrary-redirect-v2-aescripts` assert a 301 every 30 minutes, so the next failure
raises an alarm instead of waiting for a support email.

## Do NOT delete this site — users with old CEP installs depend on these redirects.

## Related

- Main repo: `jamesxdigital/emoji-library`
- Cloudflare Pages projects: `emojilibrary-gumroad`, `emojilibrary-aescripts`
