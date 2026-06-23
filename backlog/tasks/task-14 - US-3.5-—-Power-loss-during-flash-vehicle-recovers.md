---
id: TASK-14
title: 'US-3.5 — Power loss during flash, vehicle recovers'
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-3
dependencies: []
ordinal: 14000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Power cuts during flashing never leave the vehicle unbootable.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Power hard-cut at 30%, 60%, and 90% through the flash
- [ ] #2 A/B partitions ensure the previous firmware boots cleanly after each cut
- [ ] #3 Incomplete partition is not marked bootable
- [ ] #4 Update resumes and completes after power is restored
<!-- AC:END -->
