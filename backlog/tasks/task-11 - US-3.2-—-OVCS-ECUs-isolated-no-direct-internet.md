---
id: TASK-11
title: 'US-3.2 — OVCS ECUs isolated, no direct internet'
status: To Do
assignee: []
created_date: '2026-06-23 17:23'
labels:
  - user-story
  - milestone-3
dependencies: []
ordinal: 11000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
ECUs route through the gateway only; the gateway becomes the sole ingress.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 OVCS network reconfigured so ECUs route through the gateway only (default route removed)
- [ ] #2 Firewall: ECUs can reach only the OTA server via the gateway tunnel
- [ ] #3 ECUs verified unable to reach external IPs (port scans)
- [ ] #4 Network topology change documented
<!-- AC:END -->
