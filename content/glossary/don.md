---
title: DON
type: glossary
status: stable
last_updated: 2026-04-12
---

# DON (DevRev Object Notation)

DevRev's unique identifier format for all objects. Every entity in DevRev has a DON-format ID.

**Format:** `don:<namespace>:<region>:<org>/<object-type>/<id>`

**Example:** `don:identity:dvrv-us-1:devo/0:devu/30`

DON IDs are used in API requests, responses, and cross-references between objects. They encode the object type, organization, and region in the identifier itself.
