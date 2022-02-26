---
title: Configure Android WireGuard Clients
tags:
    - wireguard
    - vpn
    - cryptography
    - android
---

# Configure Android WireGuard Clients

1. Install [WireGuard for Android](https://play.google.com/store/apps/details?id=com.wireguard.android)
1. Click +
1. Choose "Create from scratch"
1. Set Interface settings
~~~ ini
Name: Tunnel name
Private key: set an existing private key or generate
Public key: set an existing public key, if you generated the public key it will already be populated
Addresses: Comma separated list of IPs to tunnel
~~~
1. Add Peer
~~~ ini
Public key: VPN_SERVER_PUBLIC_KEY
Pre-shared key: VPN_SERVER_PSK (if provided)
Endpoint: SERVER:PORT
Allowed IPs: VPN_NETWORK_IP_FOR_PEER_1/32
~~~
