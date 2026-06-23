# SOVA — Project Management Report

**Project:** SOVA — Secure OTA for Vehicular Architectures
**Programme:** STRIKE IT 2026 (Theme 1 — Cybersecurity of connected objects: vehicular platforms)
**Partners:** Spin42 (P1, coordinator) · Swarn / Citronics (P2)
**Demonstrator:** OVCS1 at A6K (CDF6000)

This is the project's delivery plan and the living Project Management Report (deliverable D1.1). Progress is added at M3 (D1.2) and a final report at M7 (D1.3). It is the reference for the work-package, deliverable, and objective codes used across the documentation.

> Codes come from the proposal: **WPn** work package, **Tn.m** task, **Dn.m** deliverable, **On** objective, **Mn** project month. **US-n.m** are the user stories that break each milestone into engineering work. Work packages, deliverables, and objectives are defined under [Work packages, deliverables and objectives](#work-packages-deliverables-and-objectives); user stories are listed under each milestone.

---

## Delivery approach

Three end-to-end milestones, each a shippable and demonstrable system. Every milestone adds exactly one layer of complexity while keeping everything before it working. This sits on top of the contractual work packages (WP1–WP7): the milestones are the build sequence, the work packages are the scope.

| Milestone | Outcome | Work packages |
|---|---|---|
| M1 | Single 4G gateway with secure OTA | WP2 · WP3 T3.1 · WP4 T4.1 |
| M2 | Dual gateways with redundancy and failover | WP3 T3.2 / T3.3 · WP5 T5.1 |
| M3 | Delta at scale with hardened security | WP4 T4.2–T4.5 · WP5 T5.2 |

---

## Work packages, deliverables and objectives

Seven work packages from the proposal, with their tasks and deliverables. Spin42 (P1) leads every work package except WP3, which Citronics (P2) leads. Months are project months (M1 = kick-off).

### WP1 — Coordination, Project Management and Reporting (M1–M6, Spin42)
- T1.1 Kick-off and coordination setup (M1)
- T1.2 Monthly steering meetings (M1–M6)
- T1.3 Reporting (M1, M3, M7)
- **D1.1** Initial report (M1) · **D1.2** Progress report (M3) · **D1.3** Final report (M7)

### WP2 — Secure OTA Architecture Design (M1–M2, Spin42)
- T2.1 Threat modelling and security requirements (M1)
- T2.2 OTA protocol and signing scheme design (M1–M2)
- T2.3 Gateway integration specification (M1–M2)
- **D2.1** OTA Security Architecture Document (M2) · **D2.2** Gateway Integration Spec (M2)

### WP3 — 4G Gateway Integration and Redundancy (M2–M4, Citronics)
- T3.1 Single gateway integration (M2–M3)
- T3.2 Dual-gateway redundancy with failover (M3–M4)
- T3.3 Secure tunnel and monitoring (M3–M4)
- **D3.1** Integrated gateway prototype (M3) · **D3.2** Redundant gateway with failover (M4)

### WP4 — Secure Delta OTA Pipeline Implementation (M2–M5, Spin42)
- T4.1 Signing, delta generation, and packaging toolchain (M2–M3)
- T4.2 Server-side management with delta/full image selection (M3–M4)
- T4.3 Vehicle-side verification, deployment, and rollback (M3–M5)
- T4.4 Multi-node orchestration (M4–M5)
- T4.5 Delta update benchmarking under real 4G (M4–M5)
- **D4.1** Signed build pipeline with delta support (M3) · **D4.2** Complete OTA system with benchmark report (M5)

### WP5 — Fault Tolerance Testing and Validation (M4–M6, Spin42)
- T5.1 Test plan and scenario definition (M4)
- T5.2 Test execution on OVCS1 (M4–M6)
- T5.3 Results analysis and security assessment (M5–M6)
- **D5.1** Test plan (M4) · **D5.2** Test results with security assessment (M6)

### WP6 — Data Management (M1–M6, Spin42)
- T6.1 Metadata schema setup (M1)
- T6.2 Ongoing data collection (M1–M6)
- **D6.1** Final dataset and metadata package (M6)

### WP7 — Valorisation / Dissemination / Exploitation (M4–M6, Spin42)
- T7.1 Defence demonstration at CDF6000, with the OVCS1 vehicle on-site at A6K (M5)
- T7.2 Open-source release and documentation (M6)
- T7.3 Exploitation roadmap (M6)
- **D7.1** Live demonstrator (M5) · **D7.2** GitHub release (M6) · **D7.3** Exploitation roadmap (M6)

### Objectives

- **O1** Secure delta OTA pipeline: 100% rejection of tampered firmware; delta transfer reduced by 90%+.
- **O2** Redundant 4G connectivity with automatic failover.
- **O3** Fault tolerance: at least 8 degraded-mode scenarios recover safely without operator intervention.
- **O4** Security architecture, threat model, and deployment guidelines aligned with the EU Cyber Resilience Act (CRA).

---

## Milestone 1 — NervesHub → single 4G gateway → OVCS firmware

**What it proves:** End-to-end OTA works. The vehicle is reachable over 4G. Updates can be pushed, cryptographically verified, and applied — including a single-node **delta** update (a NervesHub default, so we validate it early). OVCS components are still internet-facing at this stage.

**Proposal WPs covered:** WP2 (architecture design), WP3 T3.1 (single gateway), WP4 T4.1 (signing & delta-capable toolchain)

---

### User stories & tasks

**US-1.1 — Push a signed firmware to the vehicle**
- Set up NervesHub instance (self-hosted or cloud) with a test org and device
- Register OVCS1 with a unique device certificate (Ed25519 keypair)
- Build and sign a firmware bundle using the Nerves signing toolchain
- Upload firmware to NervesHub and create a deployment targeting OVCS1
- Confirm vehicle polls, downloads, verifies signature, and applies update

**US-1.2 — Integrate Citronics board as the 4G transport**
- Mount Citronics board on OVCS1 and wire to vehicle power
- Establish secure 4G tunnel from Citronics board to NervesHub server
- Route OVCS network traffic through Citronics board (replace any direct ethernet/wifi path)
- Validate end-to-end connectivity: NervesHub → 4G LTE → OVCS vehicle management ECU

**US-1.3 — Reject a tampered or unsigned firmware**
- Generate a firmware bundle signed with an untrusted or wrong key
- Attempt delivery via NervesHub and observe vehicle-side rejection
- Confirm vehicle logs the rejection event and stays on current firmware
- Document the verification error code and recovery behaviour

**US-1.4 — Automatic rollback after a bad update**
- Build a firmware that intentionally fails health-check on boot
- Deploy it and observe the A/B partition rollback mechanism
- Confirm vehicle boots last-known-good firmware automatically
- Verify NervesHub receives failure event and marks deployment as failed

**US-1.5 — Apply a delta update (NervesHub auto-diff, on by default)**
- Publish a new firmware version and let NervesHub auto-generate the xdelta3 patch against the device's current version
- Deploy the delta; vehicle downloads the patch, reconstructs the full image, verifies hash before flash
- Confirm the transfer is materially smaller than the full image
- Note: this proves the *mechanism* on a single node; at-scale benchmarking under real 4G is Milestone 3

---

### Test scenarios

| Scenario | Expected outcome |
|---|---|
| Happy path: valid signed update delivered and applied | Vehicle boots new firmware, reports version back to NervesHub |
| Tampered firmware bundle delivered | Signature mismatch detected before flash. No change to running firmware. |
| Broken firmware triggers rollback | Health-check fails on new partition. Vehicle reverts within 30s. |
| Delta update applied (single node) | Patch reconstructs full image; hash matches; transfer materially smaller than full image. |
| Network interrupted mid-download | Download resumes from checkpoint on reconnect. No corruption. |

---

### Deliverables

| Deliverable | Reference | Target |
|---|---|---|
| OTA Security Architecture Document | D2.1 | M2 |
| Integrated single-gateway prototype on OVCS1 | D3.1 | M3 |
| Signed firmware build + delta-capable packaging toolchain | D4.1 (partial) | M3 |

---

## Milestone 2 — Dual 4G gateways with redundancy and failover

**What it proves:** A second Citronics board is added. Failover is automatic and transparent. Loss of the primary gateway does not interrupt an ongoing update.

**Proposal WPs covered:** WP3 T3.2 (dual gateway redundancy), WP3 T3.3 (secure tunnel & monitoring), WP5 T5.1 (test plan)

---

### User stories & tasks

**US-2.1 — Second gateway registered and monitored**
- Mount second Citronics board on OVCS1 with independent SIM / APN
- Implement connectivity health monitoring loop (heartbeat every N seconds)
- Expose gateway status to OTA server (primary / standby / failed)
- Write unit tests for health-check state machine

**US-2.2 — Automatic failover under 10 seconds**
- Implement switchover logic: detect primary failure, activate standby gateway
- Preserve in-progress OTA session state across gateway switch
- Measure and log switchover time; target under 10 seconds
- Implement recovery: restore primary when it comes back online

**US-2.3 — Update completes despite gateway failure mid-download**
- Simulate hard power-off of primary Citronics board during active download
- Verify secondary takes over and download resumes from checkpoint
- Confirm firmware integrity after resumed download (hash verification)
- Log total additional time added by the failover event

**US-2.4 — Both gateways fail simultaneously — safe degradation**
- Simulate both boards offline during an update
- Confirm vehicle halts download safely and does not corrupt running firmware
- Verify update resumes automatically when connectivity is restored
- Log total downtime and recovery sequence

---

### Test scenarios

| Scenario | Expected outcome |
|---|---|
| Primary gateway hard-killed during idle | Standby activates in under 10 seconds. NervesHub session maintained. |
| Primary gateway killed mid-download | Secondary takes over. Download resumes from checkpoint. Update completes. |
| Both gateways offline simultaneously | Download pauses cleanly. Resumes from checkpoint on reconnect. No corruption. |
| Primary restored after secondary took over | System returns to primary-active state without disrupting any in-progress session. |

---

### Deliverables

| Deliverable | Reference | Target |
|---|---|---|
| Redundant dual-gateway prototype with measured failover | D3.2 | M4 |
| Gateway integration spec (final) | D2.2 | M2 |
| Fault tolerance test plan | D5.1 | M4 |

---

## Milestone 3 — Delta at scale + OVCS components isolated behind gateway

**What it proves:** Delta updates are benchmarked under real 4G conditions across all nodes (the delta *mechanism* was already proven on a single node in Milestone 1). OVCS ECUs no longer have direct internet access — the OTA gateway is the sole ingress point. Multi-node orchestration and the full security model are in place.

**Proposal WPs covered:** WP4 T4.2 (server-side management), WP4 T4.3 (vehicle-side verification & rollback), WP4 T4.4 (multi-node orchestration), WP4 T4.5 (benchmarking), WP5 T5.2 (test execution)

> **Note for the team:** US-3.2 (isolating OVCS ECUs from direct internet) changes the network model of OVCS itself, not just the gateway. Flag this early so Spin42 can plan for it during WP2 architecture design.

---

### User stories & tasks

**US-3.1 — Benchmark delta updates under real 4G conditions**
- Run delta deployments across the multi-node fleet under real 4G (good / moderate / poor signal)
- Server auto-selects delta vs full image based on the base version present on each vehicle
- Measure transfer-size reduction and end-to-end time vs full image; confirm reconstructed hash matches on every node
- Record results for the delta benchmark report (D4.2); target transfer-size reduction ≥ 90%

**US-3.2 — OVCS ECUs isolated — no direct internet**
- Reconfigure OVCS network so ECUs route through gateway only (remove default internet route)
- Firewall rules: ECUs can only reach OTA update server via gateway tunnel
- Verify ECUs cannot independently reach external IPs (confirm with port scans)
- Document the network topology change and update architecture doc

**US-3.3 — Multi-node orchestrated update (all ECUs)**
- Define update sequencing policy (vehicle management → bridge → infotainment)
- Implement orchestrator that tracks per-node update state
- Handle partial success: one node fails, others remain on current version
- Test concurrent update of all 3 ECUs and measure total campaign time

**US-3.4 — Replay attack rejected**
- Capture a valid signed firmware delivery session
- Re-transmit the captured session to the vehicle
- Confirm version counter / nonce mechanism rejects the replay
- Document anti-replay mechanism in security assessment

**US-3.5 — Power loss during flash — vehicle recovers**
- Hard-cut vehicle power at 30%, 60%, and 90% through the flash process
- Confirm A/B partition ensures previous firmware boots cleanly after each cut
- Verify incomplete partition is not marked bootable
- Resume and complete update after restore of power

---

### Test scenarios

| Scenario | Expected outcome |
|---|---|
| Delta update applied from version N to N+1 | Reconstructed image hash matches full firmware. Transfer size reduction ≥ 90%. |
| ECU attempts direct internet connection | All outbound traffic dropped at gateway. Only OTA server reachable. |
| Power cut at 60% through flash | Vehicle boots previous partition. No corruption. Resumes on next connection. |
| Replay attack using captured session | Version counter / nonce mismatch detected. Update rejected. No state change. |
| Simultaneous update of all 3 ECUs | Orchestrator tracks each node independently. One failure does not abort others. |

---

### Deliverables

| Deliverable | Reference | Target |
|---|---|---|
| Complete OTA system + delta benchmark report | D4.2 | M5 |
| Test results with security assessment | D5.2 | M6 |
| Live demonstrator at A6K (CDF6000) on OVCS1 | D7.1 | M5 |
| Open-source GitHub release (MIT) | D7.2 | M6 |

---

## Running throughout — continuous track (WP1 / WP6 / WP7)

Alongside the three engineering milestones, three compulsory work packages run continuously. Their deliverables are anchored to the milestone boundaries; the data they capture is a by-product of the milestone tests, not separate engineering effort.

### WP1 — Coordination & Reporting (M1–M7)
- Kick-off and monthly steering meetings
- **D1.1** Initial report (M1) · **D1.2** Progress report (M3) · **D1.3** Final report (M7)

### WP6 — Data Management (M1–M6)
- Metadata schema set up at M1 (JSON Schema, FAIR)
- Every test scenario's results captured: failover times · delta benchmarks · 4G quality metrics · logs
- **D6.1** Consolidated dataset + metadata package (M6)

### WP7 — Valorisation & Dissemination (M4–M6)
- **D7.1** Live demonstrator at A6K (M5) · **D7.2** Open-source MIT release (M6) · **D7.3** Exploitation roadmap (M6)
- Steering & technical reports at M3 / M6

---

## Deliverables at a glance — four living documents

The 15 work-package deliverables consolidate into four specialised documents, each built up across the project rather than written once at the end:

| Document | Span | Consolidates | Built up |
|---|---|---|---|
| **1. Project Management Report** (this document) | M1 → M7 | D1.1 · D1.2 · D1.3 (reports), D7.3 (exploitation roadmap, M6) | Opened at kick-off, revised at each steering milestone (M1 · M3 · M6 · M7) |
| **2. Security Architecture & Threat Model** | M1 → M6 | D2.1 (security architecture, M2), D2.2 (gateway integration spec, M2), security assessment from D5.2 (M6) | Threat model M1 → architecture & integration spec M2 → assessment M6 |
| **3. System Build & Validation Report** | M2 → M6 | D3.1 · D3.2 (gateway + failover), D4.1 · D4.2 (delta OTA + 4G benchmark), D5.1 · D5.2 (test plan & results) | Single gateway M3 → redundancy M4 → delta M5 → validated results M6 |
| **4. Data & Open-Source Release Package** | M1 → M6 | D6.1 (test dataset + metadata, M6), D7.1 (live demo, M5), D7.2 (GitHub MIT release, M6) | Metadata schema M1 → data collected each test → demo M5 → release M6 |

---

## Reporting

| Report | Milestone | Notes |
|---|---|---|
| D1.1 Initial report | M1 | This document |
| D1.2 Progress report | M3 | Extends this document |
| D1.3 Final report | M7 | Extends this document |

Steering reviews take place at M1, M3, M6, and M7. Day-to-day progress against the milestones and user stories is tracked in the [backlog](backlog/); this report consolidates it at each steering review.