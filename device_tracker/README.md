# Presence detection

Components:
* [bluetooth device tracker](https://home-assistant.io/components/device_tracker.bluetooth_tracker/)
* [GPSlogger](https://home-assistant.io/components/device_tracker.gpslogger/)
* [nmap device tracker](https://home-assistant.io/components/device_tracker.nmap_tracker/)

You can read about [my approach here](https://blog.ceard.tech/2018/01/home-assistant-and-basic-presence.html)

## Bluetooth

Relatively short range, but unlike WiFi devices don't turn this off when they go into deep sleep. Still good enough to cover almost all the house from one corner, because the house is mostly plasterboard (aka drywall) internally.

## GPS Logger

For knowing (roughly) where people are. This is used for the proximity and travel time sensors, and other automations.

## nmap

Used for detecting when devices are home, from mobile devices to media players. Modern smart phones turn their WiFi off when they go into deep sleep though, so by itself it's not reliable.
