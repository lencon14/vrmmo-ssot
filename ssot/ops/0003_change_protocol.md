# Change Protocol (ssot_organize)

This document defines the minimal change protocol for `ssot_organize` to prevent drift.
It is process-only. It does not define new canon.

## Canonical reference
- The only canonical reference is `ssot_tag` in `vrmmo-novel/SSOT_LOCK.yml@main`.
- Reasoning MUST be based only on files reachable via that `ssot_tag` (tag-fixed). Do not treat HEAD/main as canon.

## Issue-first
- Any change (add/update/remove docs, workflows, or operational rules) MUST start as an issue.
- Each issue MUST include:
  - `ssot_tag:` (the tag being referenced)
  - evidence paths (repo paths under that tag)
- Do not infer unread content. Unknown/TBD goes to backlog/blocked.

## Adopt-only
- Do not newly decide undefined canon (world settings, story content, or unverified facts).
- Only adopt/align to already-canonical or already-agreed operational rules.
- If a request implies new canon: stop and route to backlog/blocked.

## Issues gate (novel=doing 1 / ssot=doing 0)
- Doing is managed ONLY in `vrmmo-novel` and must remain exactly 1 open issue labeled `status:doing`.
- `vrmmo-ssot` must keep `status:doing` = 0.
- `status:next` in `vrmmo-ssot` is allowed only when the issue body contains a link to the current novel doing issue, recommended first line:
  `novel_doing: https://github.com/lencon14/vrmmo-novel/issues/<number>`

## Release / lock update
After any change in `vrmmo-ssot` that should be referenced by the novel side:
1) Cut a new snapshot tag in `vrmmo-ssot`.
2) Update `vrmmo-novel/SSOT_LOCK.yml@main` to that tag (`ssot_tag`).
3) `dg_recover.ps1` MUST succeed before continuing.