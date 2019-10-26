# Home Assistant (0.88.2) configuration - Z-Wave node
This is my [Home Assistant](https://home-assistant.io/) configuration for my Z-Wave node, I'm currently running 0.88.2 (and is unlikely to change, since this install only runs my Z-Wave). It is installed on a Raspberry Pi 3, using the old All in One installer (effectively a [manual install like this](https://blog.ceard.tech/2017/12/installing-home-assistant-in-virtual.html), on a 16 GB card, that I've [upgraded to Python 3.6](https://blog.ceard.tech/2017/12/upgrading-python-virtual-environment.html). I use a [Razberry](https://razberry.z-wave.me/) board for Z-Wave control.

The configuration for my primary instance [can be found here](https://github.com/DubhAd/Home-AssistantConfig). The primary instance uses [Home Assistant Remote](https://github.com/lukas-hetzenecker/home-assistant-remote) to connect to this instance.

To limit the risk brought by SD card corruption (a known risk with Pi3) I store the Home Assistant database on a USB stick, and use a multi-port USB charger with sufficient power for all ports, but have left one unused. The power cables are short, and high quality, to minimise issues with voltage drop. Of course, I also take [many different backups](https://blog.ceard.tech/2017/10/backing-up-home-assistant.html) to reduce the risk of losing anything.

This is one of a number of Pi3s I've got, and they're all in a [Multi-Pi stackable case](https://www.modmypi.com/raspberry-pi/cases-183/multi-pi-stacker/multi-pi-stackable-raspberry-pi-case), to keep the footprint down. They share an HDMI cable to a nearby monitor, and an old USB keyboard I've got kicking around, because having a Pi fail to respond isn't that uncommon.

Each directory has a short readme explaining what's in there, and the purpose of each file or group of files.

## On this Pi I run

* [Home Assistant](https://home-assistant.io/)

## The devices, services, and software I use with this Pi

* [Sandisk Extreme](https://www.sandisk.co.uk/home/memory-cards/microsd-cards/extreme-microsd) micro SD cards
* [Z-Wave](https://home-assistant.io/docs/z-wave/)
  * Z-Wave.me [Razberry](https://razberry.z-wave.me/) Z-Wave board - it has the advantage of not using a USB port, but does require that the onboard Bluetooth is disabled
  * Aeotec [MultiSensor 6](https://aeotec.com/z-wave-sensor)
  * Fibaro [motion sensor](https://www.fibaro.com/en/products/motion-sensor/) in the living room
  * Fibaro FGK10x door sensors (previous generation, superseded by the [FGDW-002](http://manuals.fibaro.com/door-window-sensor-2/)) on the garage doors
  * Sensative [door/window strips](https://www.stripsbysensative.com/strips-guard/) on the external house doors
  * TKB [TKB TZ69E](http://www.tkbhome.com/?cn-p-d-271.html) - metering wall plugs
  * Foxx Project [Smart Switch](https://www.getfoxx.com/products) (which identifies itself as an Aeotec ZW075, aka Smart Switch Gen5). These are cheap, but there's no local switch control for the attached device. Mostly I'm using these as range extenders.
  * NodOn [Octan Remote](http://nodon.fr/en/z-wave/octan-remote_7-2) in the master bedroom to provide manual control of the Yeelight. It was originally used by the kitchen door, where the next item is now mounted.
  * NodOn [Soft Remote](https://nodon.fr/en/nodon/z-wave-soft-remote/) in the second bedroom, to also provide manual control of that room's Yeelight.
  * Z-Wave.me [WALLC-S](http://eng.z-wave.me/index.php?id=30) wall controller, to provide a wall switch for the garden lights

### Other software

* [netdata](https://my-netdata.io/) so I can keep an eye on the performance
* [rpi-clone](https://github.com/billw2/rpi-clone) for bootable backups
* [rclone](https://rclone.org/) for offsite backups
* [rsnapshot](https://rsnapshot.org/) runs on another system, and pulls backups 

## Notes

* These are (automatically) modified versions of my actual configurations
