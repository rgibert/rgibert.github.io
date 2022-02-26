---
title: Installing Wireguard on Synology
tags:
    - wireguard
    - vpn
    - synology
    - cryptography
---

# Installing Wireguard on Synology

1. Download the correct release of runfalk's Synology WireGuard package from [https://github.com/runfalk/synology-wireguard/releases](https://github.com/runfalk/synology-wireguard/releases) for your device
1. Copy the spk to your Synology
1. Install the spk
~~~ bash
sudo synopkg install PATH_TO_SPK
~~~
1. Start the package
~~~ bash
sudo synopkg start WireGuard
~~~
