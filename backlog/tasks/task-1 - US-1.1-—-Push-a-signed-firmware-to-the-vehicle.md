---
id: TASK-1
title: US-1.1 — Push a signed firmware to the vehicle
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-1
dependencies: []
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
End to end: push a signed firmware from NervesHub to the vehicle, verified and applied.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 NervesHub instance set up with a test org and device
- [ ] #2 OVCS1 registered with a unique Ed25519 device certificate
- [ ] #3 Firmware bundle built and signed with the Nerves toolchain
- [ ] #4 Firmware uploaded and a deployment created targeting OVCS1
- [ ] #5 Vehicle polls, downloads, verifies signature, and applies the update
<!-- AC:END -->
