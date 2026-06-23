---
id: TASK-3
title: US-1.3 — Reject a tampered or unsigned firmware
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
updated_date: '2026-06-23 18:22'
labels:
  - user-story
  - milestone-1
milestone: m-0
dependencies: []
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
A firmware not signed by us is refused before flash.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Firmware bundle signed with an untrusted or wrong key prepared
- [ ] #2 Delivery attempted and rejected vehicle-side
- [ ] #3 Rejection logged; vehicle stays on current firmware
- [ ] #4 Verification error and recovery behaviour documented
<!-- AC:END -->
