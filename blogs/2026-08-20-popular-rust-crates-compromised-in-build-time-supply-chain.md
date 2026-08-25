---
title: "Popular Rust Crates Compromised in Build-Time Supply Chain Attack"
url: "https://socket.dev/blog/popular-rust-crates-compromised?utm_medium=feed"
date: "2026-08-20"
author: "Socket Research Team"
feed_url: "https://socket.dev/api/blog/feed.atom"
---
A threat actor compromised legitimate Rust crates and injected a malicious proc-macro1 dependency that executed cross-platform malware automatically during Cargo builds. Socket’s Threat Research Team analyzed a coordinated supply chain attack affecting three legitimate Rust crates maintained by David Roundy ( droundy ): arrayref@0.3.10 internment@0.8.7 append-only-vec@0.1.9 Socket’s AI Scanner independently detected the malicious proc-macro1 crate on August 20, 2026 at 07:29:50 UTC. At that point only arrayref@0.3.10 had been republished with the malicious dependency; malicious internment@0.8.
