# Quizzes

Self-check quizzes organized by general topic, not by "what you personally
did" — the questions are written so anyone learning the topic could use
them, not just you. That's intentional groundwork for a future project:
a web app where someone picks a topic (Git, GitHub, caching, whatever)
and gets quizzed on it.

Each file under `topics/` is meant to stand alone as one topic's worth of
content, with a small frontmatter block (`topic`, `description`) that a
future app could parse directly to build a topic list.

## Format

Every topic file has:
- A frontmatter header (`topic`, `description`)
- Numbered questions
- An answer key below a horizontal rule, so you can attempt it before
  peeking

## How this works

1. Pick a topic, answer the questions in your own words first.
2. Check the answer key.
3. Tell Claude how it went — what you knew solidly, what needed a nudge,
   what you got wrong.
4. Claude logs the attempt in `results.md`.

Results are a record for you, not a grade — the point is finding gaps
before an interview does.

## Topics available

- `topics/git.md` — staging, commits, branching, merge conflicts
- `topics/github-and-cicd.md` — pull requests, GitHub Actions, what CI/CD
  actually means
- `topics/http-and-rest.md` — HTTP methods, status codes, REST design
- `topics/dns-and-deployment.md` — DNS resolution, records, static site
  deploys
- `topics/browser-internals.md` — DOM, rendering pipeline, DevTools,
  cookies/sessions
- `topics/json-and-data.md` — JSON syntax rules, schema validation

More topics get added here as later phases introduce them (e.g. caching,
databases, React state management, auth).

## Log

See `results.md` for the full history of attempts.

## Roadmap

The end goal is a real web app: topics as a browsable list, questions
served as actual quizzes (possibly multiple-choice), user accounts, and
results tracked per-user online instead of in a markdown log.

These markdown files are the content source for that, written to convert
cleanly later — one topic per file, one frontmatter block per topic,
numbered questions with a clear correct answer already spelled out in the
answer key (which is most of the work needed to derive multiple-choice
distractors down the line). Nothing about auth/hosting/UI is built yet;
that's future scope once there's enough topic content to make an app
worth building.

**Difficulty tiers and locking.** Every topic file has a `difficulty`
field in its frontmatter (`beginner`, `intermediate`, or `advanced`),
roughly tracking which phase of the learning plan introduced it. In the
eventual app, each user has a progress level, and harder topics stay
locked until the easier topics below them are completed — so someone
can't jump to an advanced topic (e.g. auth, caching) without having
cleared the beginner ones it builds on (e.g. HTTP, REST). Right now all
existing topics are `beginner` (Phase 0/1 fundamentals); tiers will rise
as topics from later phases get added.
