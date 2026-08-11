# Learning Progress

Tracks progress against the Full Stack Engineering Learning Plan in Notion:
https://app.notion.com/p/Full-Stack-Engineering-Learning-Plan-ebf9bc7b01a9827086428166e908d796?source=copy_link

Last synced with Notion + repo state: 2026-08-11.

## Current phase

**Phase 1: Your Digital Home Base — Git, GitHub, and Your Personal Site**

Phase 0 (How the Web Works) is marked DONE in Notion.

## Completed

- Astro project initialized and pushed to GitHub
- Required Project 1 (Personal Blog Site) underway:
  - Home, About, and Blog pages built (`src/pages/index.astro`, `about.astro`, `blog/index.astro`, `blog/[...slug].astro`)
  - Blog content collection set up with Markdown (`src/content/blog/`)
  - First blog post written: "Why I am Learning to Code"
  - About page bio content added
- Branch → PR → merge workflow demonstrated (PR #1 "first-blog-post", PR #2 "update-about-page", both merged to `master`)
- Site is live on Vercel, custom domain (`moneerabedrabbo.com`) is registered (confirmed by user 2026-08-11)
- `astro.config.mjs` `site` field updated from placeholder to `https://moneerabedrabbo.com` (2026-08-11)
- PR #3 (home page rebuild, social constants sync, blog post cleanup) and PR #4 (domain fix) merged to `master`; Vercel auto-deployed and live sitemap confirmed serving `moneerabedrabbo.com` URLs (2026-08-11)

## In progress

- None — `master` is caught up with the latest merged work.

## Not yet done (per Phase 1 checklist)

- Basic GitHub Action for PR build checks — no `.github/workflows/` directory exists yet
- GitHub profile README — can't verify from this repo
- Merge conflict resolution — no evidence yet either way (may not have come up)
- 2 more Phase 1 blog posts (have 1 of 3 chosen ideas written)

## Notes / recurring gaps

- Cloudflare DNS is presumably managing the registered domain per CLAUDE.md deployment notes, but not yet verified directly.
