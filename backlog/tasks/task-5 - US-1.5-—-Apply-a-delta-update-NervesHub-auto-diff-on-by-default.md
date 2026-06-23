---
id: TASK-5
title: 'US-1.5 — Apply a delta update (NervesHub auto-diff, on by default)'
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
updated_date: '2026-06-23 18:22'
labels:
  - user-story
  - milestone-1
milestone: m-0
dependencies: []
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Validate the delta mechanism on a single node. At-scale benchmarking is Milestone 3.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 New version published; NervesHub auto-generates the xdelta3 patch
- [ ] #2 Vehicle downloads the patch, reconstructs the image, verifies hash before flash
- [ ] #3 Transfer is materially smaller than the full image
<!-- AC:END -->
