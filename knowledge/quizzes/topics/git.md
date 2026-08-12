---
topic: Git
description: Staging, commits, branching, and resolving merge conflicts.
difficulty: beginner
---

# Git

## Questions

1. What's the difference between `git add` and `git commit`? What state is
   a change in after each one?
2. What's the difference between `git commit` and `git push`?
3. What do the `<<<<<<<`, `=======`, and `>>>>>>>` markers mean when Git
   reports a merge conflict?
4. Why is it risky to resolve a conflict by just picking one side without
   reading both?
5. What makes a merge commit structurally different from a normal commit?
6. What's the difference between `git branch -d` and `git branch -D`?
7. What does `git status` tell you that `git diff` doesn't, and vice versa?
8. What's the difference between a local branch and a remote-tracking
   branch (e.g. `origin/main`)?
9. Why does `git log --graph` show two lines converging at a merge commit?
10. What's a fast-forward merge, and why doesn't it create a merge commit?

---

## Answer Key

1. `git add` stages a change — it marks it to be included in the next
   snapshot, but nothing permanent is recorded yet. `git commit` takes
   everything staged and saves it as a permanent snapshot in the local
   history. After `add`: staged but not committed. After `commit`:
   permanent locally, but still not shared anywhere else.
2. `commit` saves a snapshot to your local history only. `push` uploads
   any commits not yet on the remote so others can see them. A commit is
   already permanent before it's ever pushed — push is purely about
   publishing it.
3. Everything between `<<<<<<<` and `=======` is your current branch's
   version of the conflicting lines. Everything between `=======` and
   `>>>>>>>` is the incoming branch's version. `<<<<<<<` and `>>>>>>>`
   mark the boundaries of the whole conflict block.
4. The conflict exists because both branches changed something meaningful
   in the same spot — blindly taking one side can silently throw away
   real work from the other branch. Only reading both versions lets you
   judge which change (or combination) is actually correct.
5. A merge commit has **two parent commits** instead of one — it's the
   single point where two divergent lines of history rejoin.
6. `-d` (lowercase) deletes a branch only if it's already fully merged —
   it refuses otherwise, which makes it the safe default. `-D`
   (uppercase) force-deletes regardless of merge status, which can lose
   unmerged commits.
7. `git status` shows *which files* have changed (staged, unstaged,
   untracked) but not what changed inside them. `git diff` shows the
   actual line-by-line changes. Use `status` to see the lay of the land,
   `diff` to see the content.
8. A local branch is a pointer on your machine that moves as you commit.
   A remote-tracking branch like `origin/main` is a local snapshot of
   where that branch was on the remote as of your last fetch/pull — it
   only updates when you talk to the remote.
9. Because a merge commit has two parents, the graph draws one line per
   parent leading into that commit — visually, that's two branches
   joining into a single node.
10. A fast-forward merge happens when the target branch hasn't diverged at
    all — it has no new commits of its own since the branch being merged
    split off. Git can just move the branch pointer forward to the tip of
    the other branch instead of creating a new commit, because there's
    nothing to actually reconcile.
