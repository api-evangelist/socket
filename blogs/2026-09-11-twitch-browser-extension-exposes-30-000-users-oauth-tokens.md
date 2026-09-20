---
title: "Twitch Browser Extension Exposes 30,000 Users’ OAuth Tokens to Russian Bot Service"
url: "https://socket.dev/blog/malicious-twitch-browser-extension?utm_medium=feed"
date: "2026-09-11"
author: "Kush Pandya"
feed_url: "https://socket.dev/api/blog/feed.atom"
---
Update, September 16, 2026: After publication, the JeetBot team reached out to us. They acknowledged the security risk of the token handling and that the extension's store description and privacy policy did not adequately disclose it, and they released a fix. We confirmed the remediation in the code: Firefox version 85.8.7 no longer forwards the viewer's Twitch OAuth token to the proxy (the auth parameter is now hardcoded to empty and auth-token parameters are stripped).
