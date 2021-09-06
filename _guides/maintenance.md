---
layout: page
title: Maintenance
description: Maintaining the Makerbot Replicator 1
order: 3
---

# {{ page.title }}

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

### Useful Links

* [The Makerbot Replicator™ - Support](https://web.archive.org/web/20130126145337/http://www.makerbot.com/support/replicator)
* [Original MakerBot REPLICATOR 1 REPAIR PARTS & ACCESSORIES Page](https://web.archive.org/web/20130118060753/http://store.makerbot.com/parts-accessories/replicator-1-repair-parts-accessories.html)
* [The Replicator Maintenance](https://www.youtube.com/watch?v=HA5TvWp5YJ8) [YouTube]

### Lubrication

Use a very light coat of PTFE grease on the 6 precision rods, threaded Z-axis rod and the X-axis idler pulleys.

### Heater cartridges

24V 40-45W cartridge to fit a ¼ inch (6.35 mm) diameter hole. The diameter of a cartridge will be around 0.247 inches (6.27 mm) with a tolerance of plus or minus .002 inches (0.05 mm). The approximate wire length needed from control board to mounted cartridge is 51 inches (1.3m). Heater cartridge lead lengths are shorter than that so extension leads will need to be spliced. Ensure that the cartridges are 24V.  They will have a resistances of 13-15 Ohms across the wires.

### Thermocouples

K-Type thermocouple

### Replacing Extruder Nozzles

* [REPLACING YOUR MK8 NOZZLE](https://web.archive.org/web/20121205043439/http://www.makerbot.com/support/replicator/troubleshooting/nozzle-swap/)

Use 0.4mm MK8 nozzles. Never try to replace a nozzle cold! Always do a preheat and remove the nozzle hot. Trying to remove it cold is a guaranteed way to shear one off!
{:.ui.small.warning.message}

The nozzles on dual-extruder Replicators are adjusted at our factory to be within 0.3 mm of each other's heights, but if you want to fine-tune them, click [here](https://web.archive.org/web/20121201020214/http://www.makerbot.com/support/replicator/troubleshooting/support/replicator/troubleshooting/nozzle-shim) to learn how to use a Kapton tape shim to raise one side of the Stepstruder.


### Changing the WiFi on the Raspberry Pi (OctoPrint)


Remove the SD card, plug it into another Linux computer like e.g., the Raspberry Pi and enter in Terminal:
Use an Ethernet cable to connect your Pi with your router directly.

In order to change the WiFi settings on the Raspberry Pi, you will need to connect to edit and edit the WiFi settings file.

#### Connect a HDMI monitor and USB keyboard to access the Linux console

* Enter login credentials, default `pi` and `raspberry`

* Edit the WiFi settings file

```bash
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

* Change the WiFi settings

```
network={
   ssid="Test Wifi Network"
   psk="SecretPassWord"
}
```

#### Connect an ethernet cable between your computer and the Raspberry Pi, then use a terminal emulator to connect

* Once the cable has been connected, open your terminal emulator
* Connect to the raspberry pi

```bash
ssh pi@octopi.local
```

* Enter your password, then proceed as shown above

#### Remove the microSD card from the Raspberry Pi and insert in your computer

The `wpa_supplicant.conf` should be in the `/boot` folder on the SD card

---

## Design Files

The Makerbot Replicator 1 was open source:

* [The MakerBot Replicator](https://www.thingiverse.com/thing:18813)
* [MakerBot Replicator Interface Board REVB](https://www.thingiverse.com/thing:16067)
* [MakerBot Replicator Heater Board REVB](https://www.thingiverse.com/thing:16061)
* [MakerBot MightyBoard RevE](https://www.thingiverse.com/thing:16058)
* [MakerBot BotStep17 REVE](https://www.thingiverse.com/thing:16059)

## Modifications

* [Mk8 Spring loaded Drive Block Replicator 1](https://www.thingiverse.com/thing:231310)
* [Active Cooling Fan Duct v2 for Replicator 1](https://www.thingiverse.com/thing:537918)
* [Replicator Power Cord Support Bracket](https://www.thingiverse.com/thing:29761)
* [Scorpio Spy - Raspberry Camera holder for 3d print CTC - FlashForge and Other](https://www.thingiverse.com/thing:2117003)
* [Dial Indicator Mount For Replicator](https://www.thingiverse.com/thing:26389)