---
name: GitHub repo tree snapshots
description: Reliable multi-repository inventory through the GitHub App connector.
---

**Rule:** Fetch recursive Git trees sequentially through the GitHub App proxy, and filter tree entries or discussion responses before logging instead of returning full payloads.

**Why:** A concurrent batch produced secondary 429 responses while the primary rate-limit quota remained high. Logging a full tree or lengthy issue thread can also overwhelm the response and truncate useful state.

**How to apply:** When comparing repositories, request one tree at a time and reduce it to only relevant paths, blob IDs, and sizes. Summarize issue comments and PR files in the sandbox; return only the instructions, status, and evidence needed for the next step.
