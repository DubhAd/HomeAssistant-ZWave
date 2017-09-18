# Home Assistant configuration
This is my [Home Assistant](https://home-assistant.io/) configuration. It is installed on a Raspberry Pi 3, using the [All in One installer](https://home-assistant.io/docs/installation/raspberry-pi-all-in-one/), on a 16 GB card. I use a [Razberry](https://razberry.z-wave.me/) board for Z-Wave control.

To limit the risk brought by SD card corruption (a known risk with Pi3) I use a multi-port USB charger with sufficient power for all ports, but have left one unused. The power cables are short, and high quality, to minimise issues with voltage drop. For backups I use a USB micro-SD reader and [rpi-clone](https://github.com/billw2/rpi-clone) to provide live-boot backups, [rsnapshot](http://rsnapshot.org/) for on-site backups (from another Pi3), and [rclone](https://rclone.org/) for offsite backups to [Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html).

**On the Pi itself I run**

* [Home Assistant](https://home-assistant.io/)
* [Floorplan](https://github.com/pkozul/ha-floorplan) for a high level overview
* [HA Dashboard](https://appdaemon.readthedocs.io/en/latest/DASHBOARD_INSTALL.html) for a "finger friendly" interface
* [nginx](https://nginx.org/en/) to provide remote access, in conjunction with [Let's Encrypt](https://letsencrypt.org/)
* [rpi-clone](https://github.com/billw2/rpi-clone) for bootable backups
* [rclone](https://rclone.org/) for offsite backups
* [pi-hole](https://pi-hole.net/) so I can easily block "smart" devices from calling home
* [mosquitto](https://mosquitto.org/) to provide local MQTT services, and bridge to [CloudMQTT](https://www.cloudmqtt.com/)
* [netdata](https://my-netdata.io/) so I can keep an eye on the performance
