# Home Assistant (0.75.3) configuration
This is my [Home Assistant](https://home-assistant.io/) configuration, I'm currently running 0.75.3. It is installed on a Raspberry Pi 3, using the old All in One installer (effectively a [manual install like this](https://blog.ceard.tech/2017/12/installing-home-assistant-in-virtual.html), on a 16 GB card, that I've [upgraded to Python 3.6](https://blog.ceard.tech/2017/12/upgrading-python-virtual-environment.html). I use a [Razberry](https://razberry.z-wave.me/) board for Z-Wave control.

To limit the risk brought by SD card corruption (a known risk with Pi3) I store the Home Assistant database on a USB stick, and use a multi-port USB charger with sufficient power for all ports, but have left one unused. The power cables are short, and high quality, to minimise issues with voltage drop. Of course, I also take [many different backups](https://blog.ceard.tech/2017/10/backing-up-home-assistant.html) to reduce the risk of losing anything.

This is one of a number of Pi3s I've got, and they're all in a [Multi-Pi stackable case](https://www.modmypi.com/raspberry-pi/cases-183/multi-pi-stacker/multi-pi-stackable-raspberry-pi-case), to keep the footprint down. They share an HDMI cable to a nearby monitor, and an old USB keyboard I've got kicking around, because having a Pi fail to respond isn't that uncommon.

Each directory has a short readme explaining what's in there, and the purpose of each file or group of files.

## On the Pi itself I run

* [Home Assistant](https://home-assistant.io/)
* [Floorplan](https://github.com/pkozul/ha-floorplan) for a high level overview
  * ![Screenshot of floorplan](https://i.imgur.com/LEUpofO.png)
  * Showing: 
    * The blue bin is being collected tomorrow (yellow outline), and the brown bin in 2 or more days (green outline). The grey bin isn't currently scheduled for collection. 
    * The background lighting in the lounge is on, as is the light by the house number. 
    * The utility door is open, and the garden lights are on. Other exterior doors are closed.
    * The TV and Chromecast are off, as are the Sonos speakers.
    * The TV and X-Box in the family room are on. 
    * All the mobiles are home, as is the tablet. 
    * Oh, and the printer isn't yet low on consumables.
  * The floorplan was created in [Inkscape](https://inkscape.org/), by importing the image of the house's floorplan from the purchase paperwork, then drawing over it. If you look [at it](www/custom_ui/floorplan/floorplan.svg) you'll see that I built it up in layers, one for the foundation (ground), one for the structure, and one for the sensors. I don't really use those currently, other than to ensure that the right things are on top (sensors).
* [HA Dashboard](https://appdaemon.readthedocs.io/en/latest/DASHBOARD_INSTALL.html) for a "finger friendly" interface
  * ![Screenshot of HA Dashboard](https://i.imgur.com/gEvzY9x.png)
* [nginx](https://nginx.org/en/) to provide remote access, in conjunction with [Let's Encrypt](https://letsencrypt.org/)
* [rpi-clone](https://github.com/billw2/rpi-clone) for bootable backups
* [rclone](https://rclone.org/) for offsite backups
* [pi-hole](https://pi-hole.net/) so I can easily block "smart" devices from calling home
* [netdata](https://my-netdata.io/) so I can keep an eye on the performance

## The devices, services, and software I use (with HA)

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
* Lighting
  * [Yeelight](https://home-assistant.io/components/light.yeelight/) component and [led strips](https://www.yeelight.com/en_US/product/pitaya), one mounted behind the headboard in the master bedroom, and one along the wall side of the bed frame in the second bedroom. These provide good enough lighting to read by at night, and also to help wake us in the morning.
  * Outdoor mains [240V LED strip](https://www.lightingever.co.uk/220-240-v-ac-led-strip-multicolour-5050-50m.html) which we turn on and off with one of the wall plugs
  * [Philips Hue](https://www.home-assistant.io/components/hue/) compatible LED strips built following [this guide](https://char.gd/blog/2018/building-better-cheaper-philips-hue-led-strips), using the [Gledopto GL-C-008](https://www.aliexpress.com/item/GLEDOPTO-ZIGBEE-Led-Controller-Amazon-Echo-hue-lightify-tradfri-compatible-LED-controller-RGB-CCT-WW-CW/32858603964.html) RGB+CCT LED Controller, a roll of RGB-CCT LED tape, and a 24V power supply
  * [Philips Hue](https://www2.meethue.com/en-gb/p/hue-bridge/8718696516850) bridge (v2)
* [Google Home Mini](https://store.google.com/product/google_home_mini), with the [Google Assistant](https://home-assistant.io/components/google_assistant/) component
* Media
  * [Sonos](https://www.sonos.com/) speakers and [component](https://home-assistant.io/components/media_player.sonos/)
  * [Squeezebox Radio](http://support.logitech.com/en_us/product/squeezebox-radio-black) as a smart alarm clock, and [associated component](https://home-assistant.io/components/media_player.squeezebox/)
* Notifications:
  * [HTML5 push](https://home-assistant.io/components/notify.html5/), alongside [Pushover](https://pushover.net/) for lightweight notifications to phones/tablets, and for rich notifications I'm experimenting with [Slack](https://slack.com/)
  * [LaMetric](https://lametric.com/) for [notifications](https://home-assistant.io/components/notify.lametric/) "in person", and it's a clock the rest of the time
  * [TTS](https://home-assistant.io/components/tts/) with the Google Home Mini's, Sonos, and Squeezeboxes
* Presence detection:
  * Back to using [Nmap](https://nmap.org/) for [device tracking](https://home-assistant.io/components/device_tracker.nmap_tracker/). While I did switch to [Fritz!Box](https://en.avm.de/) [device tracking](https://www.home-assistant.io/components/device_tracker.fritz/) when I upgraded my router, the router ran out of memory
  * [CSL Bluetooth adapter](https://www.amazon.co.uk/gp/product/B00VFT4LD2/) for the [Bluetooth device tracker](https://home-assistant.io/components/device_tracker.bluetooth_tracker/), to augment the Nmap device tracker (uses a CSR8510 A10 chip)
  * [GPS Logger](https://home-assistant.io/components/device_tracker.gpslogger/) for remote device tracking
    * I used to use [OwnTracks](http://owntracks.org/) for device tracking, using the [HTTP interface](https://home-assistant.io/components/device_tracker.owntracks_http/), but not only does it have an [annoying bug](https://github.com/owntracks/android/issues/508) that causes it to randomly disable reporting, but it's been abandoned by the developer
* [TransportAPI](https://developer.transportapi.com/) for information on the local train service with the [UK transport](https://home-assistant.io/components/sensor.uk_transport/) component
* [DarkSky](https://darksky.net/dev/) for weather data, alongside the [Met Office](https://www.metoffice.gov.uk/datapoint), along with the [associated](https://home-assistant.io/components/sensor.darksky/) sensor [components](https://home-assistant.io/components/sensor.metoffice/)
* [Plex](https://www.plex.tv/sign-in/) for watching media, on TV, tablets and mobiles. I don't currently use [the component](https://home-assistant.io/components/media_player.plex/)
* [Xbox Live sensor(https://home-assistant.io/components/sensor.xbox_live/) which uses the [XBoxAPI](https://xboxapi.com/) to track when one of us is on the XBox
* [Google Travel Time component](https://home-assistant.io/components/sensor.google_travel_time/) which uses the Google [Distance Matrix](https://developers.google.com/maps/documentation/distance-matrix/) to provide estimated time to home
* [Getmail](http://pyropus.ca/software/getmail/) with [a script](local/bin/parse-email) that acts as the message delivery agent, to parse the recycling collection emails
  * I gave up on the the [IMAP email content](https://home-assistant.io/components/sensor.imap_email_content/) sensor since it doesn't keep state through restarts (which isn't unique to it, Home Assistant doesn't have a persistence mechanism other than for the `input_*` entities)
* A HiWatch IPC-T140 dome camera, using the generic camera component. It's a 4K camera, and the Pi3 can't keep up when I use the FFMPEG component. I use the camera's built in motion detection, writing to a 200 GB SMB share (there's a firmware issue apparently, if the share is above that the camera gets confused and won't write).

### Other software

* [PiVPN](http://www.pivpn.io/) for remote access to my network
* [Pi Hole](https://pi-hole.net/) for blocking those pesky adverts

## Presence detection

* If you were following along, you'll note I use three different device trackers, two for home (nmap, bluetooth) and one for away (GPSLogger). I explain more about [this here](https://blog.ceard.tech/2018/01/home-assistant-and-basic-presence.html), with an update [here](https://blog.ceard.tech/2018/09/a-while-back-i-covered-how-i-was-doing.html). Short version - I don't use groups, or merge the trackers. Both of those approaches have major shortcomings, for the first if you have a misbehaving sensor that's stuck at `home` you'll never be marked as away. For the second, the last one to update wins, so you can flip flop between two states. I'm experimenting with the [Bayesian](https://www.home-assistant.io/components/binary_sensor.bayesian) sensor and some automation logic.

## Notes

* These are (automatically) modified versions of my actual configurations
* The goals with Home Assistant have been:
  1. Minimise human actions, and where that isn't possible streamline those human actions
  2. Provide voice control where the automations don't get it right (but try to fix that)
  3. Have a minimal UI (HA Dashboard currently) to provide manual control

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
* [My blog](https://ceard.tech/) on home automation and other things

# Coffee

If I've helped you, and you really want to, you can [buy me a coffee](https://buymeacoff.ee/9MWvkxr8P), but don't feel obliged - I'm not doing this for free coffee ;)
