---
title: "Setting Up CI/CD for a Static Site: From Zero to Auto-Deploy"
description: "My site already deployed automatically on push. What it didn't have was a check that a pull request actually builds before merging, so I wrote one by hand and tested it for real."
pubDate: "Aug 12 2026"
---

My site already had half of "CI/CD" without me really setting anything up: Vercel watches my GitHub repo, and every time I push to `master`, it automatically builds and deploys the new version. That's continuous deployment. But I didn't have the other half: nothing was checking that a pull request actually *builds* before it gets merged. I could merge something completely broken and only find out when the live site went down.

So I wrote a GitHub Action by hand to close that gap: a workflow that runs on every pull request and fails loudly if the site doesn't build.

The file lives at `.github/workflows/build-check.yml`. GitHub only looks in that exact path. The workflow itself is short: it triggers `on: pull_request`, spins up a fresh Ubuntu machine, checks out my code, installs Node, runs `npm ci`, then runs `npm run build`. If any of those steps fail, the check fails, and it shows up right on the PR.

My first draft had a bug I didn't catch by eye. YAML determines structure entirely from indentation, no brackets, no keywords, and I'd indented my last two steps one space deeper than the first two. To me it looked like a formatting quirk. To the YAML parser, it was ambiguous whether those lines were new steps at all. I only found it because I checked the raw whitespace character by character instead of trusting how it looked in the editor.

Once it was fixed, I didn't just assume it worked. I tested it for real. I pushed the workflow on its own branch, opened an actual pull request, and watched the Actions tab run every step live: checkout, setup-node, `npm ci`, `npm run build`, all green. GitHub marked the PR "All checks have passed," and I merged it.

That last part felt like the actual lesson. It's easy to write a workflow file that *looks* right. The only way to know it *is* right is to watch it run against a real PR and see it pass, or better, see it correctly fail once, so you know it's actually checking something.
