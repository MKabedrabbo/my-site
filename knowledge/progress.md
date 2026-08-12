# Learning Progress

Tracks progress against the Full Stack Engineering Learning Plan in Notion:
https://app.notion.com/p/Full-Stack-Engineering-Learning-Plan-ebf9bc7b01a9827086428166e908d796?source=copy_link

Last synced with Notion + repo state: 2026-08-12.

This file is now kept current automatically as we work — Claude updates it
with key points after each session rather than waiting to be asked.

## Current phase

**Phase 1: Your Digital Home Base — Git, GitHub, and Your Personal Site — COMPLETE**

Milestone 1 fully checked off (2026-08-12). Only remaining Phase 1 work is
optional (3 blog posts). Next up: Phase 2 — Programming Fundamentals
(JavaScript and TypeScript).

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
- Git basics quiz passed (2026-08-11): explained staging area (`git add`) vs. commit, `git status` vs. `git diff`, and the commit-vs-push distinction (commit = permanent local snapshot, push = publishing it to the remote). Needed a nudge on "commit already being permanent, not just pending."
- **Milestone 1 item — resolved a merge conflict without losing work (2026-08-12).** Practiced hands-on: created `practice/branch-a` (changed a line to "Python") and `practice/branch-b` (same line to "Rust") from a shared ancestor, merged branch A cleanly into `master`, then merged branch B to intentionally trigger a conflict. Resolved it in VS Code's merge UI (kept "Python"), staged with `git add`, completed with `git commit -m "..."`. Confirmed the merge commit has two parents via `git log --graph`. Practice branches (`practice/branch-a`, `practice/branch-b`) and file (`knowledge/practice-conflict.md`) were kept as a record rather than cleaned up — the practice commits are local-only on `master`, not yet pushed to `origin/master`.
- **README overhaul (2026-08-12).** Replaced the default Astro starter README in `my-site` with a professional bio, skills section, stack, and project summary aimed at employers. Deliberately avoided claiming anything not yet true (e.g. didn't claim CI existed until it actually did — see below).
- **GitHub profile README created (2026-08-12).** New repo `github.com/MKabedrabbo/MKabedrabbo` (the special profile-repo name GitHub renders on the profile page) with a short bio linking out to `moneerabedrabbo.com`.
- **Milestone 1 item — GitHub profile has a meaningful README — closed (2026-08-12).**
- **GitHub Action build check — built from scratch and verified live (2026-08-12).** Wrote `.github/workflows/build-check.yml` by hand (typed manually, not generated) — triggers on `pull_request` to `master`, runs `actions/checkout`, `actions/setup-node` (Node 22), `npm ci`, `npm run build`. First draft had a YAML indentation bug (last two steps indented one space deeper than the first two, which breaks sequence parsing) — caught and fixed before testing. Verified for real via PR #5: pushed branch `add-build-check-workflow`, opened the PR, watched the job run live in the Actions tab (checkout → setup-node → npm ci → npm run build, all green), confirmed "All checks have passed," then merged to `master`. The workflow is now genuinely running on every PR, matching what the README claims.

## Milestone 1 checklist (Phase 1) — ALL COMPLETE

- [x] Site is live at custom domain
- [x] Pushing to `main` automatically deploys a new version
- [x] Can create a branch, make changes, open a PR, merge it, and see the deploy
- [x] Can resolve a merge conflict without losing work (2026-08-12)
- [x] GitHub profile has a meaningful README (2026-08-12)

## Skills demonstrated so far (from Notion notes + hands-on work)

**Phase 0 — Web fundamentals (all milestones complete):**
- DNS resolution chain (browser cache → OS cache → recursive resolver → root → TLD → authoritative), record types (A, CNAME, MX, TXT), TTL/propagation
- HTTP request/response cycle, methods (GET/POST/PUT/PATCH/DELETE) with safe vs. idempotent distinctions, status code ranges (2xx/3xx/4xx/5xx), the 401-vs-403 and 201/204-after-POST/DELETE conventions
- REST API design (nouns in URLs, verbs via HTTP methods), JSON syntax rules
- Cookies and sessions (`HttpOnly`, `Secure`, session IDs vs. stored passwords)
- Browser internals: DOM vs. HTML source, rendering pipeline (parse → DOM → CSS → layout → paint), DevTools tabs (Elements/Console/Network/Application)
- Terminal navigation, npm/package.json/node_modules, `.env` files and environment variables, schema validation (client vs. server)

**Phase 1 — Git, GitHub, deployment (all milestones complete):**
- Git: init/add/commit/branch/merge, resolving real merge conflicts without data loss
- GitHub: pull requests, GitHub Actions CI (hand-written workflow, not scaffolded), profile README mechanics
- Deployment: Vercel auto-deploy on push, custom domain + DNS via Cloudflare
- Astro: content collections, Markdown-based blog posts, file-based routing

## In progress

- 3 Phase 1 blog posts (choose from 4 ideas): "What Actually Happens When You Push to GitHub," "Git for Absolute Beginners," "Setting Up CI/CD for a Static Site," "DNS Explained." None written yet — the existing "Why I am Learning to Code" post was the separate required intro post, not one of these.

## Not yet done (per Phase 1 checklist)

- 3 Phase 1 blog posts (see above) — optional before moving to Phase 2, but the plan recommends finishing them first

## Notes / recurring gaps

- Cloudflare DNS is presumably managing the registered domain per CLAUDE.md deployment notes, but not yet verified directly.
- Learned the difference between running commands via the `!` prefix in chat (visible to both) vs. a separate terminal window (not visible unless pasted) — was initially unclear on this.
- Caught a real gap between claimed vs. actual repo state (2026-08-12): README claimed GitHub Actions CI existed before it actually did. Fixed by building the real workflow rather than editing the claim away. Worth double-checking future README/site claims against actual repo state before publishing.
