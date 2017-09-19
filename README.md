# Home Assistant configuration
This is my [Home Assistant](https://home-assistant.io/) configuration. It is installed on a Raspberry Pi 3, using the [All in One installer](https://home-assistant.io/docs/installation/raspberry-pi-all-in-one/), on a 16 GB card. I use a [Razberry](https://razberry.z-wave.me/) board for Z-Wave control.

To limit the risk brought by SD card corruption (a known risk with Pi3) I use a multi-port USB charger with sufficient power for all ports, but have left one unused. The power cables are short, and high quality, to minimise issues with voltage drop. For backups I use a USB micro-SD reader and [rpi-clone](https://github.com/billw2/rpi-clone) to provide live-boot backups, [rsnapshot](http://rsnapshot.org/) for on-site backups (from another Pi3), and [rclone](https://rclone.org/) for offsite backups to [Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html).

## On the Pi itself I run

* [Home Assistant](https://home-assistant.io/)
* [Floorplan](https://github.com/pkozul/ha-floorplan) for a high level overview
* [HA Dashboard](https://appdaemon.readthedocs.io/en/latest/DASHBOARD_INSTALL.html) for a "finger friendly" interface
* [nginx](https://nginx.org/en/) to provide remote access, in conjunction with [Let's Encrypt](https://letsencrypt.org/)
* [rpi-clone](https://github.com/billw2/rpi-clone) for bootable backups
* [rclone](https://rclone.org/) for offsite backups
* [pi-hole](https://pi-hole.net/) so I can easily block "smart" devices from calling home
* [mosquitto](https://mosquitto.org/) to provide local MQTT services, and bridge to [CloudMQTT](https://www.cloudmqtt.com/)
* [netdata](https://my-netdata.io/) so I can keep an eye on the performance
* [LaMetric](https://lametric.com/) a clock and low resolution display
* [Nmap](https://nmap.org/) to support device tracking

## The devices I use

* Z-Wave.me [Razberry](https://razberry.z-wave.me/) Z-Wave board - it has the advantage of not using a USB port, but does require that the onboard Bluetooth is disabled
* Z-Wave Vision Garage Door detector - these are tilt sensors
* Aeotec [MultiSensor 6](https://aeotec.com/z-wave-sensor)
* Fibaro [motion sensor](https://www.fibaro.com/en/products/motion-sensor/)
* Sensative [door/window strips](https://www.stripsbysensative.com/strips-guard/)
* TKB [TKB TZ69E](http://www.tkbhome.com/?cn-p-d-271.html) - metering wall plugs
* NodOn [Octan Remote](http://nodon.fr/en/z-wave/octan-remote_7-2)
* Z-Wave.me [WALLC-S](http://eng.z-wave.me/index.php?id=30) wall controller
* Yeelight [led strip](https://www.yeelight.com/en_US/product/pitaya)
* Outdoor mains [240V led strip](https://www.lightingever.co.uk/220-240-v-ac-led-strip-multicolour-5050-50m.html) which we turn on and off with one of the wall plugs
* [CSL Bluetooth adapter](https://www.amazon.co.uk/gp/product/B00VFT4LD2/) to augment the Nmap device tracker

## The services and other software I use

* [LaMetric](https://lametric.com/) for notifications "in person"
* [Pushover](https://pushover.net/) for lightweight notifications to phones/tablets, alongside [HTML5 push](https://home-assistant.io/components/notify.html5/), and for rich notifications I'm experimenting with [Slack](https://slack.com/)
* [OwnTracks](http://owntracks.org/) for device tracking, combined with [CloudMQTT](https://www.cloudmqtt.com/) so I don't have to expose another service
* [TransportAPI](https://developer.transportapi.com/) for information on the local train service
* [DarkSky](https://darksky.net/dev/) for weather data, alongside the [Met Office](https://www.metoffice.gov.uk/datapoint)
* [Plex](https://www.plex.tv/sign-in/) for watching media, on TV, tablets and mobiles
* [XBoxAPI](https://xboxapi.com/) to track when one of us is on the XBox
* Google [Distance Matrix](https://developers.google.com/maps/documentation/distance-matrix/) to provide estimated time to home
* For use with the [IMAP email content](https://home-assistant.io/components/sensor.imap_email_content/) sensor I run a local [Dovecot](https://www.dovecot.org/) IMAP sensor, [Postfix](http://www.postfix.org/) SMTP server, and [Fetchmail](http://www.fetchmail.info/) to retrieve the remote email. I do it this way because of reliability issues with using a remote IMAP server (which I suspect is a reflection of my Internet connection)

## Automations

* ToDo 

## Notes

* These are (automatically) modified versions of my actual configurations
* My primary goal is to minimise human actions, and where that isn't possible streamline those human actions

# Future plans

A large amount of this will require a rewire of the lighting circuits, so that all the light switches have a neutral wire.

## Devices

* Dimmer modules at most light switches, the exception will be the toilet (since there's a fan linked to it) and the outside light
* Switch modules for the extractor fans
* Multisensors (light/motion/humidity/temperature) in the bedrooms and bathrooms
* Multisensors (light/motion/temperature) in all other rooms
* Lots more door and window sensors, including on the garden gate
* Some form of distance sensor (ultrasonic or laser) in the garage
* BLE beacons
* Digital LED strip for the front of the garage, based upon the [Bruh Automation](https://github.com/bruhautomation/ESP-MQTT-JSON-Digital-LEDs) work
* Analogue LED strips (likely with a Z-Wave controller) for accent lighting and pathway lighting

## Automation thoughts

* Turn on extractor fans when the humidity is more than 5 points above the adjacent room, turning off once they drop to within 5 points
* During darkness, if a bathroom door is opened, turn the bathroom light on at a low level, turning up to medium when the door closes, turning it off when the person leaves
* Turn on the outside front light when the front door opens, the doorbell rings, or somebody is less than 5 minutes away, and coming home
* Other than bedrooms, when the room is in darkness and there's movement turn on the light at a very low level
* During daytime, if the lights are on for *too long* turn them off
* Seasonal use of the digital LED strip
* Flash the relevant section of the LED strip red if the garage door is opening or closing

# Useful links

* [Home Assistant documentation](https://home-assistant.io/docs/) and [component list](https://home-assistant.io/components/)
* Problems with Z-Wave delays and inconsistencies? Try [this script](https://hastebin.com/igujenogud.coffeescript) in the dev-states section and you'll see if you've problem devices - shown by an RTT value of 1,000 or more, and retries significantly more than other devices
