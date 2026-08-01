---
title: "Two Joyfill npm Beta Releases Compromised to Deliver DEV#POPPER Remote Access Trojan"
url: "https://socket.dev/blog/joyfill-npm-beta-releases-compromised?utm_medium=feed"
date: "2026-07-28"
author: "Socket Research Team"
feed_url: "https://socket.dev/api/blog/feed.atom"
---
Two npm beta releases in the @joyfill namespace contain an import-time JavaScript implant that resolves encrypted code through Tron, Aptos, and BNB Smart Chain transactions. Static analysis shows that its primary branch reaches a 77 KB Node.js remote-access trojan. A parallel branch launches a detached Node.js process, requests a separate boot payload from 23[.]27[.]13[.]43/$/boot , sends the marker header Sec-V: A9-0135-3 , decrypts the response, and evaluates it.
