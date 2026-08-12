---
topic: JSON & Data Validation
description: JSON syntax rules and the difference between syntax and schema validation.
difficulty: beginner
---

# JSON & Data Validation

## Questions

1. What are the strict rules JSON keys and string values must follow?
2. Why is `{ make: "Honda" }` invalid JSON, even though it looks
   reasonable?
3. Why is `{ "inStock": True }` invalid JSON?
4. What are the valid data types in JSON?
5. What's the difference between a JSON string and a JavaScript object in
   memory?
6. What is a schema, in the context of an API accepting data?
7. What's the difference between syntax validation and schema validation?
8. Give an example of something that's valid JSON syntax but would still
   fail a reasonable schema.
9. Why must schema validation happen on the server, even if the frontend
   already validates the form?
10. What typically happens (status code, and to the data) when incoming
    data fails schema validation?

---

## Answer Key

1. Keys must be wrapped in double quotes, never single quotes or left
   unquoted. String values must also use double quotes.
2. JSON requires every key to be a quoted string — `make` with no quotes
   at all is not valid JSON, even though it's valid as a JavaScript object
   key shorthand.
3. JSON booleans must be lowercase (`true`/`false`). `True` with a capital
   T is a JavaScript/Python-style boolean, not valid JSON.
4. String, number, boolean, `null`, array, and object.
5. JSON is a plain text string format used for transmitting or storing
   data — it has stricter rules (quoted keys, no trailing commas, etc.).
   A JavaScript object is in-memory data with looser syntax rules and can
   hold things JSON can't represent directly (functions, `undefined`,
   etc.). Converting between them is what `JSON.stringify` and
   `JSON.parse` do.
6. A schema is a rulebook that defines the required shape of incoming
   data — which fields must be present, what type each one must be, and
   any value constraints (like a price having to be greater than zero).
7. Syntax validation checks whether the JSON itself is well-formed
   (correct quotes, brackets, commas). Schema validation checks whether
   the *data inside* makes sense — right types, required fields present,
   valid values — independent of whether the syntax is technically
   correct.
8. `{"year": "banana"}` — this is syntactically valid JSON (a string value
   in the right format), but it would fail a schema requiring `year` to
   be a number.
9. Anyone can bypass a frontend form entirely and send a raw HTTP request
   directly to the API (using a tool like Postman or `curl`) — frontend
   validation only improves the experience for well-behaved clients, but
   it provides no actual security. The server is the only place that
   reliably sees every request, so it's the only place validation can be
   trusted.
10. The server typically returns `400 Bad Request`, and the invalid data
    is rejected before it ever reaches the database — it never gets
    stored or processed.
