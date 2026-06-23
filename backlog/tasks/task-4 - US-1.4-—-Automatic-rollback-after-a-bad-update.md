---
id: TASK-4
title: US-1.4 — Automatic rollback after a bad update
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-1
dependencies: []
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
A firmware that fails its boot health-check rolls back automatically via A/B partitions.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Firmware that fails health-check on boot built
- [ ] #2 A/B rollback observed on deployment
- [ ] #3 Vehicle boots last-known-good firmware automatically
- [ ] #4 NervesHub receives the failure and marks the deployment failed
<!-- AC:END -->
