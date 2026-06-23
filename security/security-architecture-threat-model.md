# SOVA — Security Architecture & Threat Model

**Project:** SOVA — Secure OTA for Vehicular Architectures (STRIKE IT 2026)
**Document:** Threat model (proposal task T2.1, M1) and the Milestone 1 architecture. This grows into the full OTA Security Architecture (D2.1, M2) and the final security assessment (from D5.2, M6).
**Phase:** Milestone 1.
**Code reference:** the work packages (WPn), tasks (Tn.m), deliverables (Dn.m), and objectives (On) named here are defined in the [Project Management Report](../PLANNING.md#work-packages-deliverables-and-objectives).

---

## 1. Threat assessment (baseline from the submitted proposal)

This section records the threat assessment as committed in the SOVA proposal. It is the project-level baseline; the per-milestone coverage follows in sections 2 and 3.

### 1.1 Context

Connected vehicles run software exposed through cellular, Bluetooth, and diagnostic interfaces. Existing OTA systems are proprietary, vendor-locked, and offer no vendor-neutral, auditable way to keep software current over a vehicle's lifetime. SOVA targets this gap with an open, multi-vendor secure update system for OVCS, delivered over redundant 4G gateways. Military vehicles increasingly use COTS components from multiple vendors, so a compromised update channel on any component is a route to pushing malicious firmware across a fleet. Securing the update channel is the core security objective.

### 1.2 Assets to protect

- Firmware integrity and authenticity on every onboard computer (the OVCS Raspberry Pi nodes: vehicle management, infotainment, bridge).
- The update channel between NervesHub and the vehicle.
- The firmware signing keys.
- Vehicle availability: an interrupted or failed update must never leave the vehicle unsafe or unable to fall back.

Out of OTA scope by design: Arduino vehicle-I/O firmware is stable and excluded from OTA.

### 1.3 Adversary goals and threat surfaces

The proposal names three classes of attack the system must resist: **interception**, **replay**, and **tampering**. Mapped to surfaces:

- The 4G link between gateway and server (interception, man-in-the-middle).
- The firmware itself in transit (tampering, substitution).
- Re-use of a previously valid update (replay).
- A compromised server or gateway attempting to push firmware it should not be able to produce.
- Physical access to the vehicle's internal network.

### 1.4 Security objectives committed in the proposal

| Ref | Objective | Measurable target |
|---|---|---|
| O1 | Secure delta OTA pipeline | 100% rejection of tampered firmware; delta transfer reduced by 90%+ |
| O3 | Fault tolerance under degraded conditions | At least 8 degraded-mode scenarios recover safely without operator intervention |
| O4 | Documentation and compliance | Security architecture, threat model, and deployment guidelines aligned with the EU Cyber Resilience Act (CRA) |

These targets are the acceptance criteria the security work is measured against. CRA alignment (O4) and the formal ≥8-scenario suite (O3) are produced across M3–M6; they are noted here so the M1 work is built consistently with them.

---

## 2. Milestone 1 architecture

Milestone 1 builds the secure spine: NervesHub, a single 4G gateway on a Citronics board, and signed firmware applied on the vehicle. Redundancy (M2) and component isolation (M3) are not part of M1.

### 2.1 Components

- **NervesHub** — the update server. Stores signed firmware and records which device runs which version. It does not hold the signing private key.
- **Citronics 4G gateway** — a Nerves device providing the vehicle's 4G uplink and connecting to NervesHub.
- **OVCS target node(s)** — the Raspberry Pi computers that receive and apply firmware. At M1 a single target is enough to prove the path, and components are still internet-facing.

### 2.2 Trust model

The vehicle only ever pulls firmware; it connects out to NervesHub and is never pushed anything it did not request. An image is applied only if its Ed25519 signature verifies against the public key built into the device at build time. Nothing the network can do causes unsigned code to run.

Key separation is the central principle. The signing private key lives only on the Spin42 build pipeline. It is never on the NervesHub server, never on the gateway, and never on a target node. Compromising any of those does not let an attacker produce valid firmware.

### 2.3 Mechanisms in place at M1

| Mechanism | Purpose |
|---|---|
| Ed25519 firmware signing, verified before flash | Authenticity and integrity of every update |
| Mutual TLS (device certificate ↔ NervesHub) | Authenticated, encrypted channel over 4G |
| A/B partitions with health-check | Automatic rollback to the last good version after a bad update |
| Resumable transfer with hash check before flash | An interrupted download cannot corrupt the running firmware |
| Pull-only update model | The vehicle is never an open inbound target |

---

## 3. Threats covered and not yet covered at Milestone 1

### 3.1 Covered by the M1 build

| Threat | Mitigation at M1 | Validated by |
|---|---|---|
| Malicious or tampered firmware | Ed25519 signature verified before flash; wrong or untrusted key is rejected | "Tampered firmware" test scenario |
| A bad update bricks the vehicle | A/B partitions; failed health-check reverts to last-known-good | "Broken firmware triggers rollback" scenario |
| Interception / man-in-the-middle on 4G | Mutual TLS between device certificate and NervesHub | Gateway online over 4G |
| Interrupted download corrupts firmware | Resumable transfer plus hash verification before flash | "Network interrupted" scenario |
| Compromised server or gateway pushes firmware | Key separation: neither holds the signing key, so neither can produce valid firmware | Key-management review |

### 3.2 Not covered yet at M1 (deferred)

These are in scope for the project but not for Milestone 1.

| Threat / property | Status | Milestone |
|---|---|---|
| Replay of a previously valid update | Mechanism (firmware UUID / version counter) introduced later | M3 (US-3.4) |
| Components reachable from the internet | Isolation behind the gateway not yet in place; gateway becomes sole ingress later | M3 (US-3.2) |
| Denial of service by blocking updates | Mitigated by dual-gateway redundancy, not present at M1 | M2 |
| Failover when a gateway is lost | Single gateway at M1, no redundancy | M2 |
| Multi-node orchestration risks | Single target at M1 | M3 |

### 3.3 Note on scope relative to the proposal

Two items here go slightly beyond the submitted text and should be confirmed with the customer rather than assumed. Component isolation behind the gateway (section 3.2) changes the OVCS network model and is not committed as an objective in the proposal; it is treated as a security strength to be agreed during the WP2 architecture work. Replay protection and CRA-aligned documentation (O4) are committed but land in M3–M6, not M1.
