---
id: TASK-7
title: US-2.2 — Automatic failover under 10 seconds
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-2
dependencies: []
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Loss of the primary gateway switches to the standby transparently.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Switchover logic detects primary failure and activates standby
- [ ] #2 In-progress OTA session state preserved across the switch
- [ ] #3 Switchover time measured and logged, target under 10 seconds
- [ ] #4 Primary restored when it comes back online
<!-- AC:END -->
