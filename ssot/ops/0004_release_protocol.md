# Release Protocol (SSoT snapshots)

This document defines the minimal release protocol for vrmmo-ssot snapshots.
It ensures that vrmmo-novel always references an immutable ssot_tag via SSOT_LOCK.yml.

## Principles
- Snapshots are immutable: `ssot_tag` MUST be a git tag pointing to a specific commit.
- Canonical reference lives in `vrmmo-novel/SSOT_LOCK.yml@main`:
  - `ssot_repo`
  - `ssot_tag`
- `vendor/ssot` is transport-only. Never treat it as canonical.

## When to release a snapshot
Release a new snapshot tag when changes in vrmmo-ssot must become the new reference basis for vrmmo-novel
(e.g., process rules, MANIFEST/ROUTER updates, guardrails, or any file that DG_RECOVER must_read/default_read depends on).

## Release steps (ssot -> novel)
1) Ensure working tree clean on `vrmmo-ssot/main`.
2) Commit changes in `vrmmo-ssot`.
3) Create a new annotated tag (snapshot):
   - Name: `ssot-snap-YYYY-MM-DD-ws1` (or `-rN` if needed)
   - Tags are immutable once published. Do not move tags.
4) Push the tag to origin.
5) Update `vrmmo-novel/SSOT_LOCK.yml@main` to set `ssot_tag` to the new snapshot tag.
6) Run `dg_recover.ps1` in vrmmo-novel and require `DG_RECOVER: SUCCESS`.
   - If DG_RECOVER fails, do not proceed. Fix lock/tag issues first.

## Guardrails / gates
- vrmmo-ssot must keep `status:doing = 0`.
- `status:next` in vrmmo-ssot requires a link to the current novel doing issue in the body (see DG Guardrail).
- If SSOT_LOCK is updated with placeholders or stale values, treat it as an incident and restore DG_RECOVER first.

## Notes on caching
- SSOT_LOCK is fetched via raw URLs; CDN staleness may occur.
- dg_recover.ps1 uses a cachebust query when fetching SSOT_LOCK to ensure fresh reads.