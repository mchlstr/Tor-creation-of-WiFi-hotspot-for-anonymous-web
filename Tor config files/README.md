# EN
# Home Tor Hotspot using Transparent Proxy

## Features
* Configured hotspot starts automatically on boot
* Default `SSID` of `HouseOfThor` and `wpa_passphrase` of `LetMeBrowse1234` should be changed in `hostapd.conf` file during setup
*
*
## Tested device:
* Raspberry Pi Zero W
* 1 Port USB Network with 3 ports USB HUB
* HDMI dongle to connect to monitor
* USB Keyboard
* Ethernet cable

## Should be compatible with
Untested:
* Raspberry Pi 3
* or using an external Wi-Fi adapter

## Installation

On fresh install


\# Download Rasbian Lite (latest version) from: https://www.raspberrypi.org/downloads/raspbian/
\# Burn Image to SD-Card
\# Boot Raspberry Pi Zero W

``sudo apt update && sudo apt upgrade``
``sudo apt install git``

git clone
# SK
# Domáci Tor Hotspot s použitím Transparentnej Proxy

## Vlastnosti
* Nakonfigurovaný hotspot sa spustí automaticky pri štarte
* Predvolené `SSID` pre` HouseOfThor` a `wpa_passphrase` pre` LetMeBrowse1234` by sa mali zmeniť v súbore `hostapd.conf` počas nastavenia

## Testované na zariadení:
* Raspberry Pi Zero W
* 1 port sieťový USB s 3 portami USB HUB
* HDMI adaptér na pripojenie k monitoru
* USB klávesnica
* Ethernetový kábel

## Malo by byť kompatibilné s
Nevyskúšané:
* Raspberry Pi 3
* alebo iné Raspberry s použitím externého Wi-Fi adaptéra
