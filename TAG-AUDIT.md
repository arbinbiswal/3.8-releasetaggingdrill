# Tag Audit

## Commands and observed state

The required history checks were run on `feature/release-tagging`:

```text
git tag
(no output)

git log --oneline --decorate --all
82535d9 (HEAD -> feature/release-tagging, origin/main, origin/HEAD, main) feat: add dummy checkout service
...

git tag --sort=-v:refname
(no output)
```

There are no tag refs in the repository today. The following findings use the exact tag-like names recorded in the inherited deployment history and release notes. They are evidence of the historical convention the team must replace, even though the refs are no longer available to inspect.

| Evidence | Problem | Team impact | Rollback or traceability risk |
| --- | --- | --- | --- |
| `release_2` | Uses an underscore and an ordinal instead of a version. The incident log also says it was lightweight and unannotated. | The name gives no indication of the code change or compatibility level. | The 2026-04-22 rollback selected an older unsupported commit, so the team could not prove that it was safe. |
| `latest-good` | A moving status label is used as a production deployment target. | Its meaning changes whenever the pointer is moved, so release records cannot remain immutable. | A future `latest-good` may resolve to a different commit than the one used during the 2026-05-04 hotfix; the original rollback target is not reproducible. |
| `v1.4.2` | A valid-looking semantic version appears only as an assumption in the deployment record, with no actual tag ref in the current repository. | Operations cannot verify that the staging promotion and production artifact were identical. | A responder may check out a nonexistent or wrong commit when attempting to reproduce the 2026-04-10 deployment. |
| `version-1.0` | Adds a word and omits the patch component, so it is not `vMAJOR.MINOR.PATCH`. | Sorting and tooling cannot reliably compare it with other releases. | An automated release or rollback selector may ignore it or order it incorrectly relative to `1.5.0`. |
| `1.5.0` | Omits the required `v` prefix while other records use prefixed names. | Scripts and human instructions need special cases for equivalent releases. | A deployment manifest or command that expects `v*` can fail to find the intended release, creating ambiguity during recovery. |
| `v2-final-FINAL` | Encodes a mutable human status in a duplicated suffix rather than a version and release metadata. | “Final” cannot communicate what changed or whether a later final build superseded it. | Auditors cannot determine which commit was actually approved, and a rollback may select an unverified candidate. |
| `stable-build` | Describes a branch/build state without a release number. | The label does not identify when or why the artifact became stable. | The deployment history records a missing deployment for it, so the team cannot reconstruct the 2026-03-15 production commit. |
| `patch-new` | Uses an informal, non-unique label for a patch. | Multiple patch releases can collide with the same name and cannot be ordered. | Rollback instructions cannot distinguish which patch was known good. |

## Remediation

Use immutable annotated tags named `vMAJOR.MINOR.PATCH`, record each tag's commit and deployment in `RELEASE-MAP.md`, and describe its changes and rollback target in `RELEASES.md`.
