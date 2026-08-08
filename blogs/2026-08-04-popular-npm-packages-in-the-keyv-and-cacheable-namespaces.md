---
title: "Popular npm Packages in the keyv and Cacheable Namespaces Compromised in Active Supply Chain Attack"
url: "https://socket.dev/blog/popular-npm-packages-in-the-keyv-and-cacheable-namespaces-compromised-in-active-supply-chain?utm_medium=feed"
date: "2026-08-04"
author: "Socket Research Team"
feed_url: "https://socket.dev/api/blog/feed.atom"
---
Socket’s Threat Research Team is tracking an active supply chain compromise affecting the widely used keyv and cacheable npm packages. On August 4, 2026, at least ten packages beginning with the keyv and cacheable namespaces and spreading to packages owned by other maintainers, were published with a malicious preinstall hook ( setup.mjs ) that downloads a standalone Bun runtime, executes an obfuscated second stage, harvests cloud and CI credentials, and republishes trojanized versions of other packages the stolen npm token can reach. The affected packages collectively account for tens of milli
