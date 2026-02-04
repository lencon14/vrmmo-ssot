# DG_SSOT_RULES (Backlog receiver in vrmmo-ssot)

## Purpose
This repo receives SSoT-side backlog/next/blocked issues.
Doing is managed ONLY in vrmmo-novel (status:doing max 1).

## Labels
- status:backlog  : parked
- status:next     : ready to be pulled ONLY when linked to the novel doing issue
- status:blocked  : blocked (should include reason and link)

## Mandatory link when promoting to status:next
When applying label status:next, the issue body must include a URL:
https://github.com/lencon14/vrmmo-novel/issues/NUMBER

## Forbidden
- status:doing is forbidden in this repo.
