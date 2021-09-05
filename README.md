# EN
# Home Tor Hotspot using Transparent Proxy

## Description
This project was made for subject *Cybernetics, cognitive systems and the Internet of Things* as semestral work.

Repository contains configuration files, semestral work and PowerPoint presentation of final work. Paper and presentation were co-authored with Martin Vlčák and Matúš Rusňák.

## Features
* Configured hotspot starts automatically on boot
* Default `SSID` name `HouseOfThor` and `wpa_passphrase` of `LetMeBrowse1234` should be changed in `hostapd.conf` file during setup.


## Project was made using:
* Raspberry Pi Zero W
* 1 Port USB Network with 3 ports USB HUB
* HDMI dongle to connect to monitor
* USB Keyboard
* Ethernet cable

## Preparation of WIFI hotspot for anonymous networks
1. Burn Raspbian OS
2. "Hostapd" installation and configuration
3. Installation and configuration of "udhcpd"
4. Network interface configuration
5. Installation and configuration of "tor"
6. iptables configuration
7. IP forwarding settings
8. Disable some pre-built daemons

### Set up
#### Burn Raspbian OS
1. Download Rasbian Lite (latest version) from: https://www.raspberrypi.org/downloads/raspbian/
2. Burn Image to SD-Card
3. Boot Raspberry Pi Zero W
4. Update and upgrade system

``sudo apt update && sudo apt upgrade``

#### "Hostapd" installation and configuration
1. Install hostapd

`$ sudo apt install hostapd`

2. create file`/etc/hostapd/hostapd.conf`and copy the content from `tor config files/hostapd.conf`. Change `ssid` and `wpa_passphrase` to your own

3. Edit file `etc/default/hostapd` by uncommenting list `DEAMON_CONF` and adding the absolute path to conf file. It should look like this `DEAMON_CONF="/etc/hostapd/hostapd.conf"`

4. Unmask, enable and restart hostapd deamon
```$ sudo systemctl unmask hostapd
$ sudo systemctl enable hostapd
$ sudo systemctl stop hostapd
$ sudo systemctl start hostapd
```

#### Installation and configuration of "udhcpd"
1. Install udhcpd - part of busybox

`$ sudo apt install busybox`

note: it may come preinstalled on raspian

2. Edit `/etc/udhcpd.conf` as shown in `tor config files/udhcpd.conf`and `/etc/default/udhcpd` in `tor config files/udhcpd`

3. Restart the service
```
$ sudo systemctl stop udhcpd
$ sudo systemctl start udhcpd
```

#### Network interface configuration
1. Edit `/etc/network/interfaces` as show in `tor config files/interfaces`

#### Installation and configuration of "tor"
1. Install tor package
`$ sudo apt install tor`
2. Edit configuration file `etc/tor/torrc`. For the project purposes it is enough to have just lines of file as mentioned in `tor config files/torrc`. If you want to keep original file, look for like `Log notice file /var/log/tor/notices.log` and uncomment it. For the rest of the file, copy the transparent proxy setting at the end.
3. Create the `notices.log` file change ownership to debain-tor and set permissions to 640
```
$ touch /var/log/tor/notices.log
$ chown debian-tor /var/log/tor/notices.log
$ chmod 640 /var/log/tor/notices.log
```
4. Enable the automatic start of service
`$ sudo update-rc.d tor enable`

#### iptables configuration
1. Edit iptables located in ` /etc/iptables.ipv4` as shown in `tor config files/iptables.ipv4.nat`

#### IP forwarding settings
1. Edit `etc/systcl.conf`. Either replace content of original file by content in `tor config files/sysctl.conf` or by uncommenting line `net.ipv4.ip_forward=1` to enable IP forwarding and adding the `vm.swappiness` modifier to the end of the file

#### Disable some pre-built daemons
1. Disable Avahi and dhcpcd deamons, which are interfearing with the set up
```
$ sudo systemctl disable dhcpcd
$ sudo systemctl disable avahi-daemon
```

# SK
# Tor: Tvorba wifi hotspotu pre anonymný web

## Popis
Tento projekt bol vytvorený pre predmet *Kybernetika, kognitívne systémy a internet vecí* ako semestrálna práca.

Repozitár obsahuje konfiguračné súbory, semestrálnu prácu a prezentáciu záverečnej práce. Písomná verzia semestráclnej práce a prezentácia boli napísané v spolupráci s Martinom Vlčákom a Matúšom Rusňákom.

## Vlastnosti
* Konfigurovaný hotspot sa spustí automaticky pri štarte
* Predvolený názov `SSID`` HouseOfThor` a `wpa_passphrase` súboru` LetMeBrowse1234` by sa mal počas nastavovania zmeniť v súbore `hostapd.conf`.

## Projekt bol vytvorený pomocou:
* Raspberry Pi Zero W
* 1 port USB sieť s 3 portmi USB HUB
* HDMI kľúč pre pripojenie k monitoru
* USB klávesnica
* Ethernetový kábel

## Príprava hotspotu WIFI pre anonymné siete
1. Napálenie Raspbian OS
2. Inštalácia a konfigurácia „Hostapd“
3. Inštalácia a konfigurácia „udhcpd“
4. Konfigurácia sieťového rozhrania
5. Inštalácia a konfigurácia „tor“
6. Konfigurácia iptables
7. Nastavenia presmerovania IP
8. Zakážte niektoré vopred pripravené démony

### Nastavenie a inštalácia
#### Napálenie Raspbian OS
1. Stiahnite si Rasbian Lite (najnovšia verzia) z: https://www.raspberrypi.org/downloads/raspbian/
2. Napaľte obraz na kartu SD
3. Spustite Raspberry Pi Zero W
4. Aktualizujte systém

"sudo apt update && sudo apt upgrade`

#### Inštalácia a konfigurácia „Hostapd“
1. Nainštalácia hostapd

`$ sudo apt install hostapd`

2. Vytvorte súbor `/etc/hostapd/hostapd.conf` a skopírujte obsah z `tor config files/hostapd.conf`. Zmeňte `ssid` a `wpa_passphrase` na svoje vlastné.

3. Upravte súbor `etc/default/hostapd` odkomentovaním zoznamu `DEAMON_CONF` a pridaním absolútnej cesty k súboru hostpad.conf. Malo by to vyzerať takto `DEAMON_CONF ="/etc/hostapd/hostapd.conf "`

4. Odmaskujte, povoľte a reštartujte hostapd deamon
```$ sudo systemctl odmaskovať hostapd
$ sudo systemctl povoliť hostapd
$ sudo systemctl stop hostapd
$ sudo systemctl start hostapd
```

#### Inštalácia a konfigurácia „udhcpd“
1. Nainštalujte udhcpd - súčasť busyboxu

`$ sudo apt install busybox`

poznámka: môže byť predinštalovaný na raspian

2. Upravte `/etc/udhcpd.conf` ako je uvedené v časti `tor config files/udhcpd.conf` a `/etc/default/udhcpd` v časti `tor config files/udhcpd`

3. Reštartujte službu
```
$ sudo systemctl stop udhcpd
$ sudo systemctl start udhcpd
```

#### Konfigurácia sieťového rozhrania
1. Upravte `/etc/network/interfaces` tak, ako je to uvedené v `tor config files/interfaces`

#### Inštalácia a konfigurácia súboru „tor“
1. Nainštalujte balík tor
`$ sudo apt install tor`
2. Upravte konfiguračný súbor `etc/tor/torrc`. Na účely projektu stačí mať iba riadky súboru, ako je uvedené v `tor config files/torrc`. Ak si chcete ponechať pôvodný súbor, vyhľadajte výraz `Log notice file /var/log/tor/notices.log` a zrušte jeho označenie. Pre zvyšok súboru skopírujte nastavenie transparentného servera proxy na konci.
3. Vytvorte súbor `notices.log`, zmeňte vlastníctvo suboru na debain-tor a nastavte povolenia na 640
```
$ touch /var/log/tor/notices.log
$ chown debian-tor /var/log/tor/notices.log
$ chmod 640 /var/log/tor/notices.log
```
4. Povoľte automatické spustenie služby
`$ sudo update-rc.d tor enable`

#### Konfigurácia iptables
1. Upravte iptables nachádzajúce sa v `/etc/iptables.ipv4`, ako je uvedené v `tor konfiguračných súboroch/iptables.ipv4.nat`

#### Nastavenia presmerovania IP
1. Upravte `etc/systcl.conf`. Ak chcete povoliť presmerovanie IP a pridať modifikátor `vm.swappiness` na koniec súboru, buď nahraďte obsah pôvodného súboru obsahom v konfiguračnom súbore `tor config files/sysctl.conf` alebo odkomentovaním riadka `net.ipv4.ip_forward = 1`.

#### Vypnite niektoré vopred pripravené démony
1. Vypnite Avahi a dhcpcd deamony, ktoré sú v rozpore s nastavením
```
$ sudo systemctl zakázať dhcpcd
$ sudo systemctl vypnúť avahi-daemon
```
