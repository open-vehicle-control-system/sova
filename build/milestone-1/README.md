# Milestone 1

Milestone 1 is "NervesHub to a single 4G gateway to firmware". Before the harder parts (delta, redundancy, isolation) we need the spine working: a server that holds signed firmware, and a gateway that reaches it over 4G and applies what it's told to.

Two things to stand up first:

1. [NervesHub running somewhere](01-nerveshub-deployment.md), with one org, one product, one device.
2. [The 4G gateway firmware](02-citronics-4g-gateway.md) on the Citronics Fairphone 2, online over 4G and talking to NervesHub.

Status, to update before the meeting:

| Step | State |
|---|---|
| NervesHub deployed | in progress |
| Gateway 4G uplink and routing (`wan_router`) | basic firmware working |
| Gateway connected to NervesHub | not started |

## What we can show

Once the gateway is registered with NervesHub, we can push a signed firmware over 4G and watch it apply. That's the M1 happy path (US-1.1). The gateway already does the 4G part; what's left is wiring it to NervesHub (see [step 2](02-citronics-4g-gateway.md)).

The test scenarios we check off are in [validation.md](validation.md). What changed in the firmware repos since the project started is in the [changelogs](../../changelog/).

## What comes after

Not for next week, just so the direction is clear:

- Reject tampered firmware and roll back automatically after a bad update (US-1.3, US-1.4).
- Apply a delta update on the single node. Delta is on by default in NervesHub, so we try it early (US-1.5).
- Milestone 2 adds a second gateway with automatic failover under ten seconds.
- Milestone 3 benchmarks delta at scale and isolates the nodes behind the gateway.

Full detail: [`../../PLANNING.md`](../../PLANNING.md).
