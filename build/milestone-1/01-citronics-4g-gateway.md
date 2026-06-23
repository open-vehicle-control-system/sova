# The 4G gateway firmware

The gateway is a Citronics Lime board using a refurbished Fairphone 2 running the [`wan_router`](https://github.com/open-vehicle-control-system/wan_router) firmware, a Nerves project built on the [`nerves_system_fairphone2`](https://github.com/Spin42/nerves_system_fairphone2) system. What changed since the SOVA project started is in the [changelogs](../../changelog/).

## What the firware does

`wan_router` is a NAT router. It shares an upstream internet connection with the downstream devices on its LAN (the OVCS nodes), and it keeps two WAN sources:

- WiFi client on `wlan0`, joined to an upstream access point.
- 4G modem on `wwan0`, over QMI (`vintage_net_qmi`), with the APN.

WiFi is preferred and 4G is the failover to avoid consuming 4G data when the gateway is within Wifi reach. `WanRouter.RouteMetric` keeps `wlan0` ranked above `wwan0`, so the gateway drops to cellular only when WiFi is gone. The LAN side is `eth0`, static `10.0.1.42/24`, which is where the vehicle nodes connect.

## Build and flash

```bash
git clone https://github.com/open-vehicle-control-system/wan_router.git
cd wan_router
export MIX_TARGET=nerves_system_fairphone2
mix deps.get
mix firmware.image
fastboot flash userdata wan_router.img # The first time
```

Flashing is over fastboot, with the lk2nd bootloader installed on the Fairphone 2 (see the `nerves_system_fairphone2` README).

Two things to set before building:

- WiFi credentials go in `config/.env.exs` (gitignored): `WIFI_SSID` and `WIFI_PSK`.
- The 4G APN defaults to `simbase` in `config/target.exs`. Change it to match the SIM, along with the regulatory domain for the country.
