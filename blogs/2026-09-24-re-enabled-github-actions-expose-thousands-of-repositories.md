---
title: "Re-Enabled GitHub Actions Expose Thousands of Repositories to Mini Shai-Hulud"
url: "https://socket.dev/blog/mini-shai-hulud-actions?utm_medium=feed"
date: "2026-09-24"
author: "Karlo Zanki"
feed_url: "https://socket.dev/api/blog/feed.atom"
---
Update, September 25, 2026 : both actions-cool/issues-helper and actions-cool/maintain-one-comment have been disabled on GitHub again, so workflows referencing them now fail at job setup instead of running the payload. Two actions-cool GitHub Actions, issues-helper and maintain-one-comment , were compromised and disabled during the May 2026 Mini Shai-Hulud campaign. Both became reachable again on September 16, 2026, and their release tags still point to malicious code, so every workflow that references either one by tag rather than by commit SHA is running the payload again.
