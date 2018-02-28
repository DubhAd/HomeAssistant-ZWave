# Home Assistant (0.63.3) configuration
This is my [Home Assistant](https://home-assistant.io/) configuration, I'm currently running 0.63.3. It is installed on a Raspberry Pi 3, using the old All in One installer (effectively a [manual install like this](https://blog.ceard.tech/2017/12/installing-home-assistant-in-virtual.html), on a 16 GB card, that I've [upgraded to Python 3.6](https://blog.ceard.tech/2017/12/upgrading-python-virtual-environment.html). I use a [Razberry](https://razberry.z-wave.me/) board for Z-Wave control.

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
  * Outdoor mains [240V led strip](https://www.lightingever.co.uk/220-240-v-ac-led-strip-multicolour-5050-50m.html) which we turn on and off with one of the wall plugs
* [Google Home Mini](https://store.google.com/product/google_home_mini), with the [Google Assistant](https://home-assistant.io/components/google_assistant/) component
* Media
  * [Sonos](https://www.sonos.com/) speakers and [component](https://home-assistant.io/components/media_player.sonos/)
  * [Squeezebox Radio](http://support.logitech.com/en_us/product/squeezebox-radio-black) as a smart alarm clock, and [associated component](https://home-assistant.io/components/media_player.squeezebox/)
* Notifications:
  * [HTML5 push](https://home-assistant.io/components/notify.html5/), alongside [Pushover](https://pushover.net/) for lightweight notifications to phones/tablets, and for rich notifications I'm experimenting with [Slack](https://slack.com/)
  * [LaMetric](https://lametric.com/) for [notifications](https://home-assistant.io/components/notify.lametric/) "in person", and it's a clock the rest of the time
  * [TTS](https://home-assistant.io/components/tts/) with the Google Home Mini's, Sonos, and Squeezeboxes
* Presence detection:
  * [Nmap](https://nmap.org/) to support on network [device tracking](https://home-assistant.io/components/device_tracker.nmap_tracker/)
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

### Other software

* [PiVPN](http://www.pivpn.io/) for remote access to my network

## Presence detection

* If you were following along, you'll note I use three different device trackers, two for home (nmap, bluetooth) and one for away (GPSLogger). I explain more about [this here](https://blog.ceard.tech/2018/01/home-assistant-and-basic-presence.html).

## Template sensors

* [Skalavala](https://github.com/skalavala/smarthome) provided a fantastic [template](sensors/zwave_battery_front_door.yaml) that sets the icon for the entity to a representation of the battery level. I use this for all mobile devices, and sensors.
  * ![Screenshot of battery template](https://i.imgur.com/4MnzuLM.png)
* Recycling collection [file and template sensors](sensors/bin.yaml), and [supporting script](local/bin/parse-email)
  * Notifications about upcoming collections are sent by email, the supporting script parses these emails and writes the date of the next collection for each type to it's own file, in JSON formatting
  * A file sensor for each collection type, using the above files
  * A template sensor for each collection type. This tracks whether the collection is two or more days away (future), tomorrow (tomorrow), this morning (today) or past (past). These states are used in automations, and in the HA Dashboard display.

## Automations

* Master and second bedrooms
  * Using the remote with the light strip to control the light, including dimming and colour temperature
  * Dim the light through the night, turning it to lowest brightness and red at midnight
  * Turn the light off if it was left on for half an hour
  * Turn the light on with the alarm
* Front of the house
  * Turn on the light by the house number on at dusk, and at 06:00 (or earlier if we're awake earlier than normal)
  * Turn the light off at sunrise and (just before) midnight
  * Send alerts if we've left the garage doors open for 10 minutes (and nag every 10 minutes)
  * Warn us if an outside door is opened when we're away from home
  * Warn us if the garage doors are opened once we've gone to bed
* Back of the house
  * Turn on the garden lights if the utility door is opened between dusk and dawn (elevation below -5). This temporarily turns off the "off" automations - for 8 seconds (controlled by an input_number)
  * Turn off the garden lights when the utility door is closed
  * Turn off the lights if they're left on and the door is closed
* Lounge
  * Turn on the lights when we come home and it's dark
  * Turn off the lights if we all leave (and the TV is off)
  * Turn on lights as the room gets dark (if we're home, and the TV is on)
  * Turn on the table light if motion is detected in the dark, and turn it off 2 minutes after the last motion detection
  * Mute the TV if the Sonos starts playing, and unmute when it stops
  * Stop the Sonos if the TV is turned on
  * At the end of the night, when the TV has been off for 5 minutes, or the utility door has been shut after the TV is turned off, run the bedtime script (turns of the lights one at a time)
* Hall
  * During Autumn and Winter, turn on the LED lights when the sun is below 5 degrees elevation (and we're home). Our hall is an internal hall with no windows, so it gets dark quickly.
* Home office
  * When I'm working for home, start music at the beginning of the day, and stop it at the end
* People
  * Track when we get up, go to bed, leave, and return, for other automations
  * Notify about commute delays
  * Let the adults know when the other is going to be home
* Misc
  * When battery powered sensors are getting low (25%) warn us so that we know to order a replacement, remind again at 10% and 5%
  * Check the health of the Z-Wave mesh (by looking to see that at least one device has checked in within the last 5 minutes) and run a Heal and Test if necessary
  * Send notifications on startup and shutdown of HA, and when the Z-Wave mesh is ready
  * Notify us about bin collections being due (links in with a green/amber/red Floorplan notification)
* MoreToDo 

### Garden lights

This is the most complex of my current automations, to make it "human friendly". The basic logic is that there are automations to turn the light on when the door opens, and off when it closes. To stop that simply having the light on when the door is open, it actually calls a script to turn on the lights. That script turns off the "off" automation temporarily - the duration is determined by the value of `input_number.door_delay` (in seconds).  That means that if we open and close the door (to let the dog out or going out into the garden for some other reason) the lights will stay on when the door closes.  There's another automation (and a template binary sensor) to track if the lights have been left on, and if so to turn them off. That supports a variable delay up to 2 hours, or we can just turn off the automation.

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
* [My blog](https://ceard.tech/) on home automation and other things
