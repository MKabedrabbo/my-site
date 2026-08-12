# Phase 1 Quiz — Git, GitHub, and Deployment

Based on your Notion notes for Phase 1, plus what you actually built and
shipped in `my-site` this phase.

## Questions

1. What's the difference between `git add` and `git commit`? What state is
   your work in after each one?
2. What's the difference between `git commit` and `git push`?
3. You're mid-merge and Git reports a conflict. What do the `<<<<<<<`,
   `=======`, and `>>>>>>>` markers in the file actually mean?
4. Why should you never just "take one side" of a merge conflict without
   reading it first?
5. What makes a Git commit that resolves a merge special, structurally,
   compared to a normal commit? (Hint: think about `git log --graph`.)
6. What does `git branch -d` do, and why is it safe to run on a branch
   that's already been merged?
7. What triggers the `build-check.yml` GitHub Action you wrote for
   `my-site`, and what would make it fail?
8. Why did the workflow fail the first time you wrote it, before you
   fixed it? (This one's about YAML specifically, not Git.)
9. What's the actual mechanism that makes `github.com/MKabedrabbo/MKabedrabbo`'s
   README show up on your GitHub profile page, when every other repo's
   README only shows up on that repo's own page?
10. In DNS terms, what did pointing your domain's nameservers at Cloudflare
    actually do?
11. What's the practical difference between an A record and a CNAME record
    in the context of pointing `moneerabedrabbo.com` at your host?
12. Why does Vercel deploying automatically on push to `master` count as
    "CI/CD," even though you didn't write that part yourself?

---

## Answer Key

1. `git add` stages a change — it tells Git "include this in the next
   snapshot" but doesn't record anything permanent yet. `git commit`
   takes everything staged and saves it as a permanent snapshot in your
   local history. After `add`, the change is staged but not committed;
   after `commit`, it's a permanent point you can always come back to —
   but it still only exists on your machine.
2. `commit` saves a snapshot locally — it's already permanent in your
   local history at that point. `push` is publishing that snapshot (and
   any others not yet pushed) to the remote (GitHub) so others can see
   it. Commit ≠ shared; push = shared.
3. `<<<<<<<` marks the start of *your* current branch's version of the
   conflicting lines. `=======` separates the two versions. `>>>>>>>`
   marks the end of the *incoming* branch's version. Everything between
   `<<<<<<<` and `=======` is one side; everything between `=======` and
   `>>>>>>>` is the other.
4. Blindly taking one side can silently discard real work from the other
   branch — the conflict exists because both sides changed something
   meaningful in the same spot, and Git can't know which change (or
   combination) is actually correct. Only a human reading both versions
   can decide.
5. A merge commit has **two parent commits** instead of one — it's the
   point where two divergent histories rejoin into a single line. That's
   visible in `git log --graph` as two branches converging into one node.
6. It deletes the branch pointer (the label), not any commits — since the
   branch was already merged, every commit on it is already reachable
   from `master`. `-d` (lowercase) specifically refuses to delete a
   branch with unmerged work, which is what makes it the safe version
   (`-D` force-deletes regardless).
7. It triggers on `pull_request` events targeting `master`. It fails if
   `npm ci` can't install cleanly (e.g. a broken lockfile) or if
   `npm run build` (which runs `astro build`) errors out — a type error,
   broken import, or invalid content-collection frontmatter would all
   cause that.
8. YAML sequence items (the `- uses:` / `- run:` lines under `steps:`)
   have to all sit at the *exact same indentation column*. The first
   draft had the last two steps indented one space deeper than the first
   two, so the parser couldn't tell they belonged to the same list.
9. GitHub has a specific feature: if you create a public repo whose name
   *exactly matches your username*, GitHub automatically renders that
   repo's README on your profile page instead of just on the repo page.
   It's not a setting you toggle — it's purely based on that name match.
10. It told the DNS system that Cloudflare's nameservers are now
    authoritative for that domain — i.e., "ask Cloudflare, not the
    registrar, for any DNS records related to this domain from now on."
11. An A record would point the domain directly at a fixed IP address.
    A CNAME points it at *another domain name* instead (e.g. pointing
    `www` at a host-provided domain like `cname.vercel-dns.com`), which
    is useful because the host's underlying IP can change without you
    having to update your DNS record.
12. CI/CD isn't only "a workflow file you wrote" — it's the broader
    concept of code automatically being tested/built and then deployed
    without manual steps. Vercel watching the repo and deploying on every
    push to `master` is the CD (continuous deployment) half; your
    `build-check.yml` running on PRs is the CI (continuous integration)
    half that catches problems *before* they'd ever reach that deploy.
