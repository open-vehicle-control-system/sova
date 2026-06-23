# Changelog — nerves_system_fairphone2

The Nerves system for the Fairphone 2 ([Spin42/nerves_system_fairphone2](https://github.com/Spin42/nerves_system_fairphone2)). It predates SOVA: the Fairphone 2 port is earlier Spin42 work that the gateway builds on. This lists what we changed for SOVA, from the project start on 10 June 2026.

## 2026-06-19 — Linux 6.15 kernel fork and new initramfs (`7ffb105`)

- Moved the kernel to Linux 6.15 from the `mlainez/linux-msm8x74` staging fork, which brings ADSP sensor support and Krait DVFS.
- Rebuilt against the new `citronics-initramfs` so it matches the 6.15 kernel.

Everything else (A/B rootfs layout, lk2nd bootloader, QMI modem driven from Elixir, wcn36xx WiFi) is from the pre-SOVA baseline and unchanged.
