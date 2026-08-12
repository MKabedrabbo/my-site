---
topic: Browser Internals
description: The DOM, the rendering pipeline, DevTools, and cookies/sessions.
difficulty: beginner
---

# Browser Internals

## Questions

1. What is the DOM, and how is it different from the HTML file on the
   server?
2. What are the five steps of the browser's rendering pipeline, in order?
3. What does `document.querySelector()` actually operate on, and does it
   ever touch the server?
4. Which DevTools tab would you use to see the actual HTTP requests a page
   made, and what would you check there if an API call seemed to fail?
5. Which DevTools tab would you use to check whether a cookie was set
   after logging in?
6. Why is HTTP described as "stateless," and what problem do cookies
   solve as a result?
7. Walk through what happens, step by step, when a cookie-based login
   succeeds.
8. What does the `HttpOnly` flag on a cookie protect against?
9. What does the `Secure` flag on a cookie do?
10. Why doesn't a session cookie contain your actual password?

---

## Answer Key

1. The DOM (Document Object Model) is the browser's live, in-memory tree
   built from the HTML file — it's the browser's working copy, not the
   file itself. JavaScript reads and modifies the DOM, and those changes
   are temporary: refreshing the page rebuilds the DOM from the original
   HTML source again.
2. Parse HTML → Build DOM → Apply CSS → Layout → Paint pixels.
3. It operates entirely on the DOM, inside the browser — it never talks
   to the server. Fetching data from a server and updating what's on the
   page are two separate jobs: a network request brings data in, and DOM
   methods like `querySelector` put that data onto the page.
4. The **Network** tab. For a failing API call, you'd check the request
   URL, headers, body, and the response's status code and body to see
   exactly what was sent and what came back.
5. The **Application** tab — it shows cookies and other stored data like
   local storage.
6. Stateless means the server retains no memory of previous requests —
   each request is handled independently with no built-in concept of
   "the same user as last time." Cookies solve this by letting the
   browser automatically attach an identifier to every subsequent
   request, giving the server a way to recognize returning visitors.
7. The browser POSTs credentials to a login endpoint. The server verifies
   them and responds with a `Set-Cookie` header containing a session ID.
   The browser stores that cookie automatically. On every future request
   to that site, the browser attaches `Cookie: session_id=...`. The
   server looks up that ID, finds the matching account, and treats the
   request as coming from that logged-in user.
8. It prevents JavaScript running on the page from reading that cookie's
   value — this protects against theft via a malicious or injected script
   (an XSS attack), since the script simply has no access to it.
9. It ensures the cookie is only ever sent over an encrypted HTTPS
   connection, never over plain HTTP — protecting it from being read by
   anyone snooping on the network.
10. It stores a random, meaningless session ID instead. The server keeps
    the actual mapping from that ID to the real account internally — so
    even if the cookie were stolen, the attacker only gets a string that
    identifies a session, not a password they could reuse elsewhere.
