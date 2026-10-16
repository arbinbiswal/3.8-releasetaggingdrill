# Release Map

This map ties each production release to an immutable commit and deployment record.

| Version (tag) | Commit (short hash) | Date | What Shipped |
| --- | --- | --- | --- |
| `v1.0.0` | `ff1fb9a` | 2026-06-06 | Initial checkout-service exercise scaffold, placeholder service, and baseline release documentation. |
| `v1.1.0` | `c17d4c4` | 2026-06-06 | Initial dummy checkout-service implementation. |
| `v1.1.1` | `82535d9` | 2026-06-06 | Patch refinement: names the service explicitly, reports its service version, and simplifies the startup entry point. |

## Rollback Traceability

```bash
git tag --sort=-v:refname        # the sortable release history
git checkout v1.1.0              # roll back to the last known-good tag, then redeploy
```

The annotated semantic-version sequence identifies both the exact commit and the release meaning, so `v1.1.0` is a precise, reproducible rollback target. In the original history, moving labels such as `latest-good` and ambiguous names such as `release_2` did not prove which commit was deployed, making recovery guesswork.
