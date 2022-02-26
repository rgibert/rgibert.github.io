---
title: Environment Monitoring
tags:
    - hardware
    - raspberry-pi
    - environment-monitoring
    - dht22
---

# Environment Monitoring

## Purpose

Records temperature and humidity data, to be collected using [Prometheus](https://prometheus.io/)

## Parts

- [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/)
- [DHT22 Temperature and Humidity Sensor](https://www.adafruit.com/product/385)
- [UniPiCase Zero](https://www.unipicase.com/products/unipicase-zero/)

## Assembly

- Mark off and cut the hole in the top of the case for the sensor.   
![Cut out](/assets/img/rpi/humidity/00-cut_open.jpg)
- Solder wires to the DHT22 (note, pin 3 is unused).   
![Solder wires](/assets/img/rpi/humidity/01-solder_wires.jpg)
- Tape off the exposed wires with electrical tape.   
![Protect wires](/assets/img/rpi/humidity/02-tape_off.jpg)
- Solder the wires to the Raspberry Pi Zero W.   
![Solder Pi](/assets/img/rpi/humidity/03-solder_pi.jpg)
- Push the DHT22 into the hole in the sensor, pressure should hold it into place.   
![Completed](/assets/img/rpi/humidity/04-completed.jpg)

## Setup

- Install [Raspbian](https://www.raspbian.org/)
- Edit /etc/wpa_supplicant/wpa_supplicant.conf to setup Wi-Fi:
~~~
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="wifiname"
    psk="password"
	key_mgmt=WPA-PSK
}
~~~
- Install [clintjedwards/dht22_exporter](https://github.com/clintjedwards/dht22_exporter)
- Connect Prometheus to the dht22_exporter.
- Connect Grafana to Prometheus.   
![Grafana](/assets/img/rpi/humidity/05-grafana.png)

## Notes

- Residual heat from the circuit board may increase the readings from the DHT22, you man need to calibrate the temperature with an known accurate thermometer and add an offset to the exporter.
