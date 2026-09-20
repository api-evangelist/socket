---
title: "GitHub Actions Adds cache-mode to Limit Cache Poisoning Risk"
url: "https://socket.dev/blog/github-actions-cache-mode?utm_medium=feed"
date: "2026-09-16"
author: "Sarah Gooding"
feed_url: "https://socket.dev/api/blog/feed.atom"
---
GitHub has added cache-mode to GitHub Actions , a new setting that limits how workflows and jobs can access the Actions cache. It targets cache poisoning, the technique attackers used to compromise the Ultralytics PyPI package in 2024 and the TanStack npm packages in May 2026. Cache poisoning works because an entry written to the shared Actions cache in one context can be restored and run in another.
