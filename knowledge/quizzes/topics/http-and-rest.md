---
topic: HTTP & REST APIs
description: Methods, status codes, safety/idempotency, and RESTful URL design.
difficulty: beginner
---

# HTTP & REST APIs

## Questions

1. What does it mean for an HTTP method to be "safe"? Which method(s) are
   safe?
2. What does it mean for an HTTP method to be "idempotent"? Which methods
   are idempotent, and which is not?
3. Why is `POST` neither safe nor idempotent?
4. What's the difference between `PUT` and `PATCH`?
5. What status code should a successful `POST` return, and what header
   should typically come with it?
6. What status code should a successful `DELETE` return, and why not
   `200`?
7. What's the difference between a `401` and a `403`?
8. In REST API design, why should URLs be nouns and HTTP methods be verbs?
   Give an example of a URL that violates this.
9. What does "stateless" mean in the context of REST, and what has to
   happen on every request as a result?
10. In a query string like `?limit=20&offset=40`, what's happening, and
    what pattern is this commonly used for?

---

## Answer Key

1. Safe means the request doesn't change anything on the server — it's
   read-only. Only `GET` is safe (`HEAD` and `OPTIONS` also qualify, but
   `GET` is the one people mean day to day).
2. Idempotent means making the same request multiple times produces the
   same end state as making it once. `GET`, `PUT`, `PATCH`, and `DELETE`
   are idempotent. `POST` is not.
3. Every `POST` creates a new resource — calling it twice creates two new
   resources, so the outcome changes with each call (not idempotent), and
   it modifies server state by definition (not safe).
4. `PUT` fully replaces a resource with the data provided — anything not
   included is effectively removed/reset. `PATCH` updates only the fields
   actually sent, leaving the rest untouched.
5. `201 Created`, along with a `Location` header pointing to the URL of
   the newly created resource (e.g. `Location: /users/42`).
6. `204 No Content` — the resource no longer exists, so there's nothing
   meaningful to return in the body. `200` implies a body is coming back;
   `204` explicitly signals "success, nothing to say."
7. `401 Unauthorized` means the request isn't authenticated at all — the
   server doesn't know who you are. `403 Forbidden` means you *are*
   authenticated, but you don't have permission to do this specific
   thing.
8. The HTTP method already expresses the action (the verb) — the URL only
   needs to identify *what* you're acting on (the noun/resource). A URL
   like `POST /deleteUser?id=5` violates this by putting the action in
   the URL instead of using `DELETE /users/5`.
9. Stateless means the server keeps no memory of previous requests between
   calls — each request must carry everything the server needs to process
   it (like an auth token), because the server won't remember who you
   were or what you did on the last request.
10. `limit` controls how many results to return, `offset` controls how
    many to skip before starting. Together they implement pagination —
    this example means "skip the first 40 results, return the next 20,"
    i.e. page 3 of a 20-per-page list.
