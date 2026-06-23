---
id: TASK-13
title: US-3.4 — Replay attack rejected
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-3
dependencies: []
ordinal: 13000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
A captured, previously valid update cannot be replayed.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A valid signed delivery session captured
- [ ] #2 Captured session re-transmitted to the vehicle
- [ ] #3 Version counter / nonce rejects the replay
- [ ] #4 Anti-replay mechanism documented in the security assessment
<!-- AC:END -->
