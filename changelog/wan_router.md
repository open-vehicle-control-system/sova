# Changelog — wan_router

The 4G gateway firmware ([open-vehicle-control-system/wan_router](https://github.com/open-vehicle-control-system/wan_router)). It was created for SOVA, so this is its history from the start. It builds on `nerves_system_fairphone2` (pinned to v1.33.8).

## 2026-06-19 — initial gateway

- Initial commit (`caf315c`): NAT router on the Fairphone 2 sharing an upstream connection to downstream devices on `eth0` (`10.0.1.42/24`).
- Added WiFi (`wlan0`) as an alternative WAN source alongside the 4G modem (`c37bf62`).
- Switched to a prebuilt Buildroot artifact instead of compiling the system locally (`0af0c3f`).
- `WanRouter.RouteMetric` forces WiFi above 4G, so the gateway uses cellular only as failover (`6946c99`).
- README (`b7e0187`).

## Next

Not done yet: connecting the gateway to NervesHub (`nerves_hub_link`) so it can receive signed OTA updates. That's the remaining Milestone 1 work.
