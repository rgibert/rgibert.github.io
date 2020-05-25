# Wireguard

## Install the WireGuard Synology package

1. Download the correct release of runfalk's Synology WireGuard package from https://github.com/runfalk/synology-wireguard/releases for your device
1. Copy the spk to your Synology
1. Install the spk
~~~ bash
sudo synopkg install PATH_TO_SPK
~~~
1. Start the package
~~~ bash
sudo synopkg start WireGuard
~~~

## Configure WireGuard on the Synology

1. Make sure the WireGuard module is loaded
~~~ bash
sudo modprobe WireGuard
~~~
1. Generate your public/private keys
~~~ bash
sudo sh -c 'umask 077; \
mkdir -p /etc/wireguard; \
wg genkey | tee /etc/wireguard/privatekey-$(hostname -s); \
wg pubkey > /etc/wireguard/publickey-$(hostname -s)'
~~~
1. Add the WireGuard device
~~~ bash
sudo ip link add dev wg0 type wireguard
~~~
1. Setup your configuration file at /etc/wireguard/wg0.conf

    [Interface]    
    ListenPort = 51820    
    PrivateKey = VPN_SERVER_PRIVATE_KEY    
        
    [Peer]    
    PublicKey = PEER_1_PUBLIC_KEY    
    AllowedIPs = VPN_NETWORK_IP_FOR_PEER_1/32    
        
    [Peer]    
    PublicKey = PEER_2_PUBLIC_KEY    
    AllowedIPs = VPN_NETWORK_IP_FOR_PEER_2/32    

## Configure WireGuard Clients

### Configure Android Clients

1. Install [WireGuard for Android](https://play.google.com/store/apps/details?id=com.wireguard.android)
1. Click +
1. Choose "Create from scratch"
1. Set Interface settings
~~~
Name: Tunnel name
Private key: set an existing private key or generate
Public key: set an existing public key, if you generated the public key it will already be populated
Addresses: Comma separated list of IPs to tunnel
~~~
1. Add Peer
~~~
Public key: VPN_SERVER_PUBLIC_KEY
Pre-shared key: VPN_SERVER_PSK (if provided)
Endpoint: SERVER:PORT
Allowed IPs: VPN_NETWORK_IP_FOR_PEER_1/32
~~~

### Configure Linux Clients

#### Base WireGuard Setup

1. Make sure the WireGuard module is loaded
~~~ bash
sudo modprobe WireGuard
~~~
1. Generate your public/private keys
~~~ bash
sudo sh -c 'umask 077; \
mkdir -p /etc/wireguard; \
wg genkey | tee /etc/wireguard/privatekey-$(hostname -s); \
wg pubkey > /etc/wireguard/publickey-$(hostname -s)'
~~~
1. Add the WireGuard device
~~~ bash
sudo ip link add dev wg0 type wireguard
~~~
1. Setup your configuration file at /etc/wireguard/wg0.conf

    [Interface]    
    PrivateKey = LOCAL_HOST_PRIVATE_KEY    
        
    [Peer]    
    PublicKey = SERVER_PUBLIC_KEY    
    AllowedIPs = IPS_TO_TUNNEL    
    Endpoint = SERVER:PORT    

NOTE: If you'd like to route all traffic through the VPN, set AllowedIPs to 0.0.0.0/0
1. Attach your configuration file to your WireGuard device
~~~ bash
sudo wg setconf wg0 /etc/wireguard/wg0.conf
~~~
1. Attach the VPN IP to the WireGuard device
~~~ bash
sudo ip address add dev wg0 LOCAL_HOST_VPN_IP/24
~~~
1. Bring up the tunnel
~~~ bash
sudo ip link set up dev wg0
~~~
1. Setup your routing
  - if you'd like to route just the VPN network you can simply add the following:
~~~ bash
sudo ip route add VPN_INTERNAL_NETWORK/24 dev wg0
~~~
  - if you'd like to route all traffic through the VPN, use the following:
~~~ bash
sudo ip route add 0.0.0.0/1 dev wg0
sudo ip route add 128.0.0.0/1 dev wg0
~~~

#### Gnome Toggle Setup
1. Create toggle script and save to /usr/local/bin/wireguard-toggle
NOTE: The script assumes you're in sudoers with NOPASSWD set, if not you can use [Zenity](https://help.gnome.org/users/zenity/) to add a password prompt.
~~~ bash
#!/usr/bin/env bash

set -euo pipefail

if ip a | grep -q 'wg0'; then
  for route in $(ip route | grep wg0 | cut -d" " -f1); do
    sudo ip route del ${route}
  done
  sudo ip link set down dev wg0
  sudo ip link del wg0'
else
  sudo ip link add dev wg0 type wireguard
  sudo wg setconf wg0 /etc/wireguard/wg0.conf
  sudo ip address add dev wg0 LOCAL_HOST_VPN_IP/24
  sudo ip link set up dev wg0
  sudo ip route add 0.0.0.0/1 dev wg0
  sudo ip route add 128.0.0.0/1 dev wg0
fi
~~~
1. Copy the WireGuard icon
~~~ bash
mkdir -p ~/.local/share/icons
wget https://richard.gibert.ca/assets/images/wireguard.png -P ~/.local/share/icons
~~~
1. Create the desktop file at ~/.local/share/applications
~~~
[Desktop Entry]
Type=Application
Name[en_CA]=WireGuard Toggle
Categories=System;
X-GNOME-FullName[en_CA]=WireGuard
Comment[en_CA]=Toggle WireGuard
Icon=wireguard.png
NoDisplay=false
Exec=bash -c /usr/local/bin/wireguard-toggle
Terminal=false
X-GNOME-UsesNotifications=true
~~~
1. Install [WG Indicator](https://extensions.gnome.org/extension/2027/wg-indicator/)
