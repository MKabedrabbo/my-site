# Phase 0 Quiz — Web Fundamentals

Based on your Notion notes for Phase 0 (How the Web Works). Answer these in
your own words before checking the key.

## Questions

1. What happens, step by step, when you type a URL and hit Enter? (This is
   a real, common junior-dev interview question — give the full walkthrough.)
2. What's the difference between an A record and a CNAME record?
3. What is TTL, and why would you lower it before migrating a server?
4. Is `PUT` idempotent? Is it safe? What's the difference between those two
   properties?
5. Why is `POST` the only HTTP method that's neither safe nor idempotent?
6. What status code should a successful `POST` return, and what header
   should come with it?
7. What status code should a successful `DELETE` return, and why not `200`?
8. What's the difference between a `401` and a `403`?
9. What does the `HttpOnly` flag on a cookie actually protect against?
10. Why doesn't a session cookie store your password?
11. In a URL like `spotify.com/search?q=drake&limit=20&offset=40`, what do
    `limit` and `offset` do together?
12. What's the difference between the DOM and the HTML file on the server?
13. What are the five steps of the browser's rendering pipeline, in order?
14. What's the difference between schema validation and syntax validation
    for JSON — and why must schema validation happen on the server, not
    just in the browser?
15. Why don't you commit `node_modules` to GitHub, and what do you commit
    instead so a teammate can rebuild it?

---

## Answer Key

1. Browser checks its DNS cache → if empty, goes through a recursive
   resolver → root nameserver → TLD nameserver → authoritative nameserver
   to get an IP. Browser opens a TCP connection (port 80 or 443). If
   HTTPS, a TLS handshake happens (certificates exchanged, encryption key
   agreed). Browser sends a GET request. Server responds with a status
   code (usually 200) and HTML. Browser runs the rendering pipeline: parse
   HTML → build DOM → apply CSS → layout → paint pixels — firing off
   additional requests for CSS/JS/images along the way.
2. A record maps a domain directly to an IPv4 address. CNAME maps a domain
   to *another domain name* instead of an IP.
3. TTL is how long (in seconds) a DNS record is cached before being
   re-checked. Lowering it before a migration means the new IP propagates
   faster once you switch, since caches expire sooner.
4. Yes, `PUT` is idempotent — calling it 10 times with the same data
   leaves the resource in the same end state as calling it once. It is
   *not* safe, because it changes data on the server. Safe = doesn't
   change anything; idempotent = repeating it doesn't change the outcome
   beyond the first call.
5. Every `POST` creates a new resource — call it twice and you get two new
   records, so the outcome changes each time (not idempotent), and it
   obviously modifies server state (not safe).
6. `201 Created`, with a `Location` header pointing to the new resource
   (e.g. `Location: /users/42`).
7. `204 No Content` — the resource is gone, so there's nothing to send
   back. `200` implies a body; `204` explicitly means "success, nothing
   to return."
8. `401 Unauthorized` = not logged in at all (no ID shown). `403
   Forbidden` = logged in, but not allowed to do this (showed ID, on the
   no-entry list).
9. It prevents JavaScript running on the page from reading the cookie,
   which protects against theft via a malicious/injected script (XSS).
10. It stores a random session ID, not the password itself. The server
    maps that ID to your account internally — even if the cookie is
    stolen, the attacker only gets a meaningless string, not your
    credentials.
11. `limit` = how many results to return, `offset` = how many to skip.
    Together they implement pagination — `limit=20&offset=40` means "skip
    the first 40, show the next 20" (page 3).
12. The HTML file on the server is the original source (the "recipe").
    The DOM is the browser's live, in-memory working copy built from that
    HTML (the "meal you cooked from it") — you can change the DOM without
    touching the file, and it resets on refresh.
13. Parse HTML → Build DOM → Apply CSS → Layout → Paint pixels.
14. Syntax validation checks if the JSON is *formatted* correctly (quotes,
    brackets, commas). Schema validation checks if the *values inside*
    make sense (right types, required fields present, valid ranges) —
    `{"year": "banana"}` is syntactically valid JSON but fails a schema
    requiring `year` to be a number. It must happen server-side because
    anyone can bypass a browser form and send a raw HTTP request straight
    to the API (e.g. via Postman).
15. `node_modules` is massive and fully reproducible by running
    `npm install`. You commit `package.json` (and the lockfile) instead —
    it's the "shopping list," and anyone can clone the repo and rebuild
    the "kitchen" from it.
