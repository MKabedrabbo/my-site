---
topic: DNS & Deployment
description: How domain names resolve to servers, and how modern static sites go live.
difficulty: beginner
---

# DNS & Deployment

## Questions

1. What is DNS, in one sentence, and what analogy is commonly used to
   explain it?
2. What is the full DNS resolution order, from browser cache to getting an
   IP address back?
3. What's the difference between an A record and a CNAME record?
4. What is a TXT record commonly used for?
5. What is TTL, and why would you lower it before migrating a server to a
   new host?
6. What does it actually mean to "change your nameservers" to point at a
   provider like Cloudflare?
7. Why can DNS changes take hours to fully take effect worldwide (DNS
   propagation)?
8. What does it mean for a static site generator to build HTML "at compile
   time" rather than "at request time"? What's the practical benefit?
9. What makes deploying on push to a main branch "continuous deployment,"
   as opposed to a traditional manual deploy process?
10. Why does a TLS handshake need to happen before any encrypted data can
    be sent, and what does it actually establish?

---

## Answer Key

1. DNS (Domain Name System) is a worldwide network of servers that
   translates human-friendly domain names into IP addresses. The common
   analogy is a phone book — you look up a name and get back a number.
2. Browser cache → OS cache → recursive resolver → root nameserver → TLD
   nameserver (e.g. `.com`) → authoritative nameserver, which finally
   returns the actual IP address.
3. An A record maps a domain directly to an IPv4 address. A CNAME maps a
   domain to *another domain name* instead, which is useful when the
   underlying IP might change (the host can update their end without you
   touching your DNS record).
4. Verification — proving you own a domain. A service that needs to
   confirm domain ownership typically asks you to add a specific TXT
   record as proof, since only someone with control of the DNS records
   could add it.
5. TTL (Time To Live) is how long, in seconds, a DNS record is cached
   before a resolver checks for updates again. Lowering it before a
   migration means old cached records expire faster once you switch,
   so the new IP/host propagates to visitors more quickly.
6. It tells the entire DNS system which company's servers are
   authoritative for answering any DNS questions about your domain — from
   that point on, anyone looking up your domain gets routed to that
   provider's records instead of your registrar's defaults.
7. Because DNS relies on caching at many layers (resolvers, ISPs,
   individual devices), and each cached record only expires once its TTL
   runs out — different resolvers around the world will have cached the
   old answer for different amounts of time, so the change rolls out
   gradually rather than instantly everywhere.
8. A static site generator renders all the HTML in advance, during a build
   step, and serves those pre-built files as-is on every request — as
   opposed to a dynamic server that runs code and queries a database on
   every single request to generate the page. The benefit is speed (no
   per-request computation) and simplicity of hosting (just files on a
   CDN).
9. There's no manual step between "code is merged" and "code is live" —
   the deploy is triggered automatically by the push event itself, and
   the host (e.g. Vercel) handles building and publishing without a human
   running a deploy command.
10. Without encryption established first, any data sent (passwords,
    cookies, form data) would travel as plain, readable text that anyone
    on the network could intercept. The TLS handshake lets the browser
    verify the server's identity (via its certificate) and lets both
    sides agree on a shared encryption key *before* any real data is
    exchanged, so everything after the handshake is unreadable to anyone
    else on the network.
