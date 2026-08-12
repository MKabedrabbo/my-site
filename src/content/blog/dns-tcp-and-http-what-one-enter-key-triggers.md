---
title: "DNS, TCP, and HTTP: What One Enter Key Triggers"
description: "There's a lot of steps that take place when clicking enter on a URL that you never knew about."
pubDate: "July 25 2026"
---

You ever wonder what's really happening after you type a URL and hit Enter? It seems instant, but a lot is going on behind the scenes before you see anything on the screen. There is something called DNS — Domain Name System — which works like a phone book for the internet. When you type 'google.com', you're actually looking up something closer to 192.0.0.88, but who's going to remember that? DNS lets us use names instead of numbers.

When your browser needs to find the IP address, it goes through a chain of steps. First it checks its own local cache — if you visited the site recently, it already knows the IP. If not, it reaches out to a recursive resolver, which does all the heavy lifting. The resolver asks the root nameserver, which points to the TLD nameserver (.com, .net, etc.), which finally points to the authoritative nameserver — the one that actually holds the IP address you're looking for.

Once the browser has the IP address, it opens a TCP connection to the server — on port 80 for HTTP or port 443 for HTTPS. If you're on HTTPS, there's one more step before anything loads: the TLS handshake. The browser and server exchange certificates to verify each other's identity, then agree on an encryption key. From this point on, all data sent between you and the server is encrypted — that's what the little lock icon in your browser means.

The browser then sends a GET request to the server asking for the page's content. If everything goes smoothly, the server responds with a 200 OK status code along with the HTML for the page.

But the browser isn't done yet. It runs that HTML through what's called the rendering pipeline — it parses the HTML, builds the DOM, applies CSS, calculates the layout, and finally paints pixels to the screen. As it reads through the HTML it also discovers references to other files — CSS stylesheets, JavaScript files, images — and fires off additional HTTP requests to fetch all of those too. That's why loading a single page can involve dozens of requests behind the scenes.

DNS helps us locate websites by name instead of memorizing a string of numbers — without it, we'd have to type in a random IP address for every site we visit. Knowing these steps helps you understand what's really going on under the hood, and it can help you debug issues too. For example, you've probably seen a 404 Not Found error before. That's a status code — and in my next post, I'll break down the ones you actually need to know.
