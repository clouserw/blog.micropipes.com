---
layout: post
title: Firefox Sync adds official PostgreSQL support
tags:
- Mozilla
- software
---

The Sync Storage team has landed official PostgreSQL support for Firefox Sync.

Historically, Sync has only officially supported Google Spanner as a storage backend, with MySQL working unofficially. That has been a pretty high barrier to entry for people self-hosting their own services.

With PostgreSQL support, we hope to make self-hosting more approachable and continue supporting people who want the agency of hosting their data on infrastructure they control.

There is updated documentation for running it with Docker, including a one-shot `docker compose` setup:

[https://mozilla-services.github.io/syncstorage-rs/how-to/how-to-run-with-docker.html](https://mozilla-services.github.io/syncstorage-rs/how-to/how-to-run-with-docker.html)

Mozilla is publishing Docker images for the PostgreSQL build here:

[https://ghcr.io/mozilla-services/syncstorage-rs/syncstorage-rs-postgres](https://ghcr.io/mozilla-services/syncstorage-rs/syncstorage-rs-postgres)

If you’ve been interested in self-hosting Sync but were put off by the storage requirements, take another look.  If you run into bugs or have feedback, please file issues here:

[https://github.com/mozilla-services/syncstorage-rs/issues](https://github.com/mozilla-services/syncstorage-rs/issues)
