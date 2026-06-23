---
id: TASK-12
title: US-3.3 — Multi-node orchestrated update (all ECUs)
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-3
dependencies: []
ordinal: 12000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Coordinated update across all vehicle nodes with partial-failure handling.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Update sequencing policy defined (vehicle management to bridge to infotainment)
- [ ] #2 Orchestrator tracks per-node update state
- [ ] #3 Partial success handled: one node fails, others stay on current version
- [ ] #4 Concurrent update of all 3 ECUs tested and total campaign time measured
<!-- AC:END -->
