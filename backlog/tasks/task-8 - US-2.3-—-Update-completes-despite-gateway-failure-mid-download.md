---
id: TASK-8
title: US-2.3 — Update completes despite gateway failure mid-download
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-2
dependencies: []
ordinal: 8000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
An update survives a hard loss of the active gateway during download.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Hard power-off of primary board simulated during active download
- [ ] #2 Secondary takes over and download resumes from checkpoint
- [ ] #3 Firmware integrity confirmed after resume (hash)
- [ ] #4 Additional time added by the failover logged
<!-- AC:END -->
