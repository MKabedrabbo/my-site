---
title: "DNS Explained: How Your Domain Name Finds Your Server"
description: "moneerabedrabbo.com doesn't live anywhere by that name. Here's the chain of lookups that turns a domain into an actual server, and what changing nameservers really does."
pubDate: "Aug 12 2026"
---

`moneerabedrabbo.com` doesn't live anywhere by that name. Underneath, it's just an address pointing at a server. DNS is the whole system that makes typing a name work instead of memorizing a string of numbers.

The common analogy is a phone book, and it holds up: you look up a name, you get back a number. But the actual lookup isn't one step, it's a chain. Your browser checks its own cache first. If it doesn't know the answer, it asks a recursive resolver, which asks a root nameserver, which points it to the right TLD nameserver (the one that handles `.com`), which finally points to the authoritative nameserver, the one that actually holds the real answer for your specific domain.

When I registered my domain through Namecheap, the DNS wasn't actually being managed by Namecheap by default. I pointed the nameservers at Cloudflare instead. That one change told the entire DNS system something specific: "stop asking the registrar, Cloudflare is authoritative for this domain now." Every future lookup for `moneerabedrabbo.com` gets routed to Cloudflare's records instead.

Two record types matter most for a project like this. An **A record** maps a domain straight to an IP address. A **CNAME record** maps a domain to _another domain name_ instead. That's useful because a host's underlying server IP can change without me ever having to touch my DNS settings, since I'm just pointing at their domain, not a fixed number.

The other thing that tripped me up at first: DNS changes aren't instant. Every record has a TTL (time to live): how long, in seconds, a cached answer is considered valid before it's rechecked. Different resolvers around the world cache my domain's records for different amounts of time, so a change doesn't reach everyone simultaneously. That's why people say DNS propagation can take a few hours. It's not one system updating, it's thousands of independent caches gradually expiring and re-checking.
