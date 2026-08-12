---
topic: GitHub & CI/CD
description: Pull requests, GitHub Actions, and what "CI/CD" actually means in practice.
difficulty: beginner
---

# GitHub & CI/CD

## Questions

1. What is a pull request, structurally — what two things is it comparing?
2. What triggers a GitHub Action workflow that's configured with
   `on: pull_request`?
3. In a GitHub Actions workflow, what's the difference between a "job" and
   a "step"?
4. Why do YAML-based workflows require every item in the same list (e.g.
   the steps under one job) to be indented at the exact same column?
5. What's the difference between Continuous Integration (CI) and
   Continuous Deployment/Delivery (CD)?
6. Why would a team want a build/test check to run automatically on every
   PR instead of just trusting people to run tests locally?
7. What's the special naming trick that makes a GitHub repo's README
   render on a user's profile page instead of only on the repo's own page?
8. What does `actions/checkout` do in a workflow, and why is it almost
   always the first step?
9. If a PR shows "All checks have passed" but also shows merge conflicts,
   can it still be merged? Why or why not?
10. What's the purpose of `npm ci` in a CI workflow, as opposed to
    `npm install`?

---

## Answer Key

1. A pull request compares two branches (or a fork and a branch) and
   proposes merging the changes from one into the other — it's a request
   to review and integrate a set of commits, not the commits themselves.
2. Any time a pull request is opened, or updated with new commits, against
   the branches configured (e.g. `branches: [main]`) — by default it also
   fires on other PR events like reopening, but "opened" and "synchronize"
   (new commits pushed) are the common ones people mean.
3. A **job** runs on its own fresh virtual machine and can run in parallel
   with other jobs. A **step** is one action inside a job — steps in the
   same job run sequentially, on the same machine, sharing filesystem
   state.
4. YAML determines structure purely from indentation, not from brackets or
   keywords. If list items (each starting with `-`) aren't at the same
   column, the parser can't tell whether a line is a new item in the same
   list or something nested inside the previous item — it becomes
   ambiguous or invalid.
5. CI is about automatically building/testing code whenever it changes, to
   catch problems early — the "integration" part is making sure new code
   works together with existing code. CD is about automatically shipping
   code that passes those checks to production (or close to it) without
   manual steps. CI catches problems before merge; CD gets good code out
   the door after.
6. Automated checks are consistent and can't be skipped by accident or
   forgotten under deadline pressure — a human might forget to run tests,
   or run them against stale code. A required CI check also blocks a
   broken PR from being merged at all, rather than relying on trust.
7. Creating a public repository with the *exact same name* as your GitHub
   username. GitHub detects that match and renders that repo's README on
   your profile page automatically — it's not a setting, purely a naming
   convention.
8. It downloads the repository's code onto the runner's virtual machine.
   It's first because almost every later step (installing dependencies,
   building, testing) needs the actual source files to exist on disk
   first.
9. No — merge conflicts and passing checks are two independent gates.
   Checks passing means the code builds/tests fine on its own branch;
   conflicts mean Git can't automatically combine that branch with the
   target branch's current state. Both have to be resolved before
   merging.
10. `npm ci` installs exactly what's locked in `package-lock.json`,
    deletes `node_modules` first for a clean slate, and fails outright if
    the lockfile and `package.json` are out of sync. `npm install` is more
    lenient — it can update the lockfile and doesn't guarantee a clean,
    reproducible install, which is riskier in an automated environment.
