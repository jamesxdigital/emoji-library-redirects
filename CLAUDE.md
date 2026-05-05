# CLAUDE.md - Emoji Library Redirects

Netlify redirect site for old Emoji Library CEP extension installs that still point to Netlify URLs.

## How It Works

Old ZXP builds (v2.0.1 and earlier) hardcoded Netlify branch deploy URLs. This site redirects them to the current Cloudflare Pages hosting.

- `v2-aescripts--emojilibrary.netlify.app` → `v2-aescripts.emojilibrary.jamesxdigital.com`
- `v2--emojilibrary.netlify.app` → `v2.emojilibrary.jamesxdigital.com`

## Deployment

Netlify site name: `emojilibrary`. Deployed via `netlify deploy --alias <branch> --dir=.` for each branch (`v2-aescripts`, `v2`). The `main` branch redirects to the primary domain.

## Do NOT delete this site — users with old CEP installs depend on these redirects.

## Related

- Main repo: `jamesxdigital/emoji-library`
- Cloudflare Pages projects: `emojilibrary-gumroad`, `emojilibrary-aescripts`
