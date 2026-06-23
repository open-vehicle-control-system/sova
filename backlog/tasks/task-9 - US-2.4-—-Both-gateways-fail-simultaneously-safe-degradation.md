---
id: TASK-9
title: 'US-2.4 — Both gateways fail simultaneously, safe degradation'
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
updated_date: '2026-06-23 18:23'
labels:
  - user-story
  - milestone-2
milestone: m-1
dependencies: []
ordinal: 9000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Both boards offline during an update degrades safely with no corruption.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Both boards offline during an update simulated
- [ ] #2 Download halts safely, running firmware not corrupted
- [ ] #3 Update resumes automatically when connectivity is restored
- [ ] #4 Downtime and recovery sequence logged
<!-- AC:END -->
