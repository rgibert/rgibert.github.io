---
title: Setting up WireGuard using a Synology NAS as the server
modified: 2020-04-05
tags: [wireguard, vpn]
layout: post
---

# Install the WireGuard Synology package

1. Download the correct release of runfalk's Synology WireGuard package from https://github.com/runfalk/synology-wireguard/releases for your device
2. Copy the spk to your Synology
3. Install the spk
{% highlight bash %}
synopkg install PATH_TO_SPK
{% endhighlight %}
4. Start the package
{% highlight bash %}
synopkg start WireGuard
{% endhighlight %}

# Configure WireGuard on the Synology

1. Make sure the WireGuard module is loaded
{% highlight bash %}
modprobe WireGuard
{% endhighlight %}
2. Generate your public/private keys
{% highlight bash %}
sudo sh -c "umask 077; mkdir -p /etc/wireguard && wg genkey | tee /etc/wireguard/privatekey-$(hostname -s) | wg pubkey > /etc/wireguard/publickey-$(hostname -s)"
{% endhighlight %}
3. Add the WireGuard device
{% highlight bash %}
sudo ip link add dev wg0 type wireguard
{% endhighlight %}
4. Setup your configuration file
{% highlight bash %}
echo <<EOF > /etc/wireguard/wg0.conf
[Interface]
ListenPort = 51820
PrivateKey = VPN_SERVER_PRIVATE_KEY

[Peer]
PublicKey = PEER_1_PUBLIC_KEY
AllowedIPs = VPN_NETWORK_IP_FOR_PEER_1/32

[Peer]
PublicKey = PEER_2_PUBLIC_KEY
AllowedIPs = VPN_NETWORK_IP_FOR_PEER_2/32
EOF
{% endhighlight %}

# Configure WireGuard Clients

## Configure Android Clients

1. Install [WireGuard for Android](https://play.google.com/store/apps/details?id=com.wireguard.android)
1. Click +
1. Choose "Create from scratch"
1. Set Interface settings
{% highlight bash %}
Name: Tunnel name
Private key: set an existing private key or generate
Public key: set an existing public key, if you generated the public key it will already be populated
Addresses: Comma separated list of IPs to tunnel
{% endhighlight %}
1. Add Peer
{% highlight bash %}
Public key: VPN_SERVER_PUBLIC_KEY
Pre-shared key: VPN_SERVER_PSK (if provided)
Endpoint: SERVER:PORT
Allowed IPs: VPN_NETWORK_IP_FOR_PEER_1/32
{% endhighlight %}

## Configure Linux Clients

### Base WireGuard Setup

1. Make sure the WireGuard module is loaded
{% highlight bash %}
modprobe WireGuard
{% endhighlight %}
2. Generate your public/private keys
{% highlight bash %}
sudo sh -c "umask 077; mkdir -p /etc/wireguard && wg genkey | tee /etc/wireguard/privatekey-$(hostname -s) | wg pubkey > /etc/wireguard/publickey-$(hostname -s)"
{% endhighlight %}
3. Add the WireGuard device
{% highlight bash %}
sudo ip link add dev wg0 type wireguard
{% endhighlight %}
4. Setup your configuration file
{% highlight bash %}
echo <<EOF > /etc/wireguard/wg0.conf
[Interface]
PrivateKey = LOCAL_HOST_PRIVATE_KEY

[Peer]
PublicKey = SERVER_PUBLIC_KEY
AllowedIPs = IPS_TO_TUNNEL
Endpoint = SERVER:PORT
EOF
{% endhighlight %}
  NOTE: If you'd like to route all traffic through the VPN, set AllowedIPs to 0.0.0.0/0
5. Attach your configuration file to your WireGuard device
{% highlight bash %}
wg setconf wg0 /etc/wireguard/wg0.conf
{% endhighlight %}
6. Attach the VPN IP to the WireGuard device
{% highlight bash %}
ip address add dev wg0 LOCAL_HOST_VPN_IP/24
{% endhighlight %}
7. Bring up the tunnel
{% highlight bash %}
ip link set up dev wg0
{% endhighlight %}
8. Setup your routing
  - if you'd like to route just the VPN network you can simply add the following:
{% highlight bash %}
ip route add VPN_INTERNAL_NETWORK/24 dev wg0
{% endhighlight %}
  - if you'd like to route all traffic through the VPN, use the following:
{% highlight bash %}
ip route add 0.0.0.0/1 dev wg0
ip route add 128.0.0.0/1 dev wg0
{% endhighlight %}

### Gnome Toggle Setup
  1. Create toggle script and save to /usr/local/bin/wireguard-toggle
     NOTE: The script assumes you're in sudoers with NOPASSWD set, if not you can use [Zenity](https://help.gnome.org/users/zenity/) to add a password prompt.
{% highlight bash %}
#!/usr/bin/env bash

if ip a | grep -q 'wg0'; then
  for route in $(ip route | grep wg0 | cut -d" " -f1); do
    sudo ip route del ${route}
  done
  sudo ip link set down dev wg0
  sudo ip link del wg0
else
  sudo ip link add dev wg0 type wireguard
  sudo wg setconf wg0 /etc/wireguard/wg0.conf
  sudo ip address add dev wg0 LOCAL_HOST_VPN_IP/24
  sudo ip link set up dev wg0
  sudo ip route add 0.0.0.0/1 dev wg0
  sudo ip route add 128.0.0.0/1 dev wg0
fi
{% endhighlight %}
  1. Copy the WireGuard icon
{% highlight bash %}
mkdir -p ~/.local/share/icons
wget https://richard.gibert.ca/assets/images/wireguard.png -P ~/.local/share/icons
{% endhighlight %}
  1. Create the desktop file at ~/.local/share/applications
{% highlight bash %}
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
{% endhighlight %}
  1. Install [WG Indicator](https://extensions.gnome.org/extension/2027/wg-indicator/)
