---
title: Setup WireGuard Server
tags:
    - wireguard
    - vpn
    - cryptography
    - linux
    - synology
---

# Setup WireGuard Server

1. Make sure the WireGuard module is loaded
~~~ bash
sudo modprobe WireGuard
~~~
1. Generate your public/private keys
~~~ bash
sudo sh -c 'umask 077; \
mkdir -p /etc/wireguard; \
wg genkey | tee /etc/wireguard/privatekey-$(hostname -s); \
wg pubkey < /etc/wireguard/privatekey-$(hostname -s) > /etc/wireguard/publickey-$(hostname -s)'
~~~
1. Add the WireGuard device
~~~ bash
sudo ip link add dev wg0 type wireguard
~~~
1. Setup your configuration file at `/etc/wireguard/wg0.conf`

~~~
[Interface]
ListenPort = 51820
PrivateKey = VPN_SERVER_PRIVATE_KEY

[Peer]
PublicKey = PEER_1_PUBLIC_KEY
AllowedIPs = VPN_NETWORK_IP_FOR_PEER_1/32

[Peer]
PublicKey = PEER_2_PUBLIC_KEY
AllowedIPs = VPN_NETWORK_IP_FOR_PEER_2/32
~~~
