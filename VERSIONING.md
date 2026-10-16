# Versioning Convention

## Semantic versioning

Release versions follow `MAJOR.MINOR.PATCH`:

- **MAJOR** increments for incompatible or breaking changes. Example: `v1.4.2` -> `v2.0.0`.
- **MINOR** increments for backward-compatible functionality. Example: `v1.4.2` -> `v1.5.0`.
- **PATCH** increments for backward-compatible fixes or corrections. Example: `v1.4.2` -> `v1.4.3`.

## Tag format

Every release tag uses the exact pattern `vMAJOR.MINOR.PATCH`, with numeric components and a required lowercase `v` prefix. Example: `v1.1.1`.

## Annotated release tags

Production releases use annotated tags, not lightweight tags. An annotation records the release message, tagger, and timestamp in Git, which makes the release auditable and separates an intentional release from an arbitrary pointer.

Create one with:

```bash
git tag -a v1.1.0 -m "Release 1.1.0: add checkout service"
```

## Pre-releases

Release candidates and betas append a hyphenated identifier and sequence number, such as `v1.5.0-rc.1` or `v1.5.0-beta.1`. Pre-releases sort before the corresponding final version, and sequence numbers increase (`rc.1` before `rc.2`); the final `v1.5.0` is later than all `v1.5.0-*` tags.
