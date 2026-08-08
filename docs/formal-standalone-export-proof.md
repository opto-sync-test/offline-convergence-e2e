# Independent standalone formal-methods export proof

This repository is intentionally outside the production `opto-sync` organization.
It independently consumes the merged formal-methods export contract from an
immutable production commit and proves that the source-side extraction boundary
works without repository-local state, credentials, submodules, or product-code
assumptions.

Pinned production source:

```text
opto-sync/opto-sync-clients@c6f51462fd7d2e54d2aa3e7b684b41e5a4d7e022
```

The workflow checks out that exact commit with persisted credentials disabled,
runs the production export regression harness, performs another independent
export, and recomputes every exported file size and SHA-256 from the resulting
`SOURCE_EXPORT.json`.

The proof also rejects product directories such as `clients/`, `adoption/`,
`formal/models/`, and `formal/traces/` from the standalone candidate tree. This
is deliberately separate from product convergence tests: its purpose is to
prove the extraction/package boundary that DEN-580 will use to bootstrap
`ORESoftware/formal-methods.rs`.

A source update requires changing `formal-export-pin.json` through review and
rerunning this workflow against the new immutable commit. Branch names are not
accepted as evidence.
