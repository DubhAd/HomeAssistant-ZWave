# Automations, automations everywhere, and all the brains did hurt

_Some of these were first written when I started with HA, and didn't know better. You'll find that I've used hyphens (-) in some file names and underscores (\_) to match Home Assistant in others. Mostly I'm not renaming files._

Explanations to follow

## Adults

### Away

This doesn't use the non-binary presence detection logic, yet. It has two main approaches. Either we're away, and the TVs are off (so, we're likely really away) or we've been away for at least 10 minutes. There's a conditional check to see if person one is playing on the XBox, but that bit isn't quite right yet.

It sets one or two input booleans, to track that the adults are away, or everybody is away.

### Doors open

Being replaced by the manual alarm

### Lights on

Turns the lights on when we come home if it's dark 

### Returned

This simply turns off a the booleans for the adults being away.

## Alarm

These are for enabling, disabling, and triggering the alarm.

## All

Like the automations for adult presence detection, but for the whole household

## Batteries

Battery related automations, to notify us when the batteries are running down, so we know what to buy.

## (Master bedroom) Bedhead light

### Bedhead light

These automations control the brightness, depending on the time of day/night

### Bedhead turn

These are triggered by the Z-Wave remote

## Bedtime

When we've all gone to sleep (or we're away and everybody who's home is asleep) this turns on the flag to indicate that it's bedtime

## Bin

Nags us the night before to remember to put the recycling out

## Christmas

Turns the Christmas lights on and off

## Clear

It used to do a bunch of things, but now this just turns fluxer back on at midday

## Dark

A couple of automations for the living room that turn the lights on when we're in there, and it's getting dark. Initially it'll just turn on the light behind the TV, then once it gets a bit darker it'll turn on all the background lighting.

## Garden

If the garden lights get left on (and the doors are closed) then this'll turn them off

## Home Assistant

Three of these are just to notify about HA being shut down, started, and the Z-Wave mesh being ready. The last enables Fluxer if HA is restarted after midday.

## Hall

Controls the hall lighting. Our hall has no windows or doors leading directly outside, so it gets quite dark. We've an LED string light that winds up the banister and along the railings, to provide sufficient background lighting.

## Holiday

If we're all in travelling mode, this sets the Holiday flag.

## House awake

If any of us wake up, or if the TV is turned on after we've gone to bed, this clears the bedtime flag.

## Late - fluxer

Turns fluxer off at 23:00. After this I want the bedroom lights to be in "night" mode - minimum brightness and red.

## Lounge

### Dark motion

If motion is detected when the lounge is dark, it'll turn on one light - enough to see by and not trip over pets, but not so much as to destroy night vision. Uses an input boolean so that 

### Daylight

The first turns off all the lights once the light level is high enough, regardless. The other turns off the lights if only a subset of them is on and the light level increases enough.

With all the background lighting on, the light sensor will read above the lower cutoff. During the brighter months however it's normal for only a subset of the lights to be on when we're up. If we also turn on the ceiling lights though, it'll stay below the upper cutoff.

## Master (bedroom) bedhead light

These are the automations to allow me to use my Z-Wave remote to control the light, changing the brightness level and colour temperature. [The cookbook](https://home-assistant.io/cookbook/dim_and_brighten_lights/) has the writeup of the brightness part of this.

## Moved to family room

When we get up we're usually in the living room, and then later we may move to the family room part of the same space as the kitchen. This automation detects when that happens and turns off the lights in the living room.

## Nighttime

Rather than wait for the normal timeout, if we've left the garden lights on during the early hours of the morning, it'll switch them off sooner.

## Not

These use the [Google Calendar](https://home-assistant.io/components/calendar.google/) component, to determine if it's not a work day, and turns off the booleans. Those booleans are used in some of the people specific automations

## Number sign

Living where we do, without a lit number sign people may fail to find us when it's dark. I'm not so worried about friends and family, more taxis and takeaway delivery ;)

These automations ensure the light is on when it needs to be (basically, sunset to midnight, then 06:00 to sunrise).

## People

The first set are for the non-binary presence detection. Some template sensors to track whether we've just left, are away, have just returned, or are at home

### Person One

#### Radio

A set of automations to control the bedside light (a Yeelight strip) depending on the state of the radio. From a maximum brightness bright white wakeup call, to a dull red glow as sleep hopefully approaches.

#### Bedside

Another set of automations, using another Z-Wave remote, to control the brightness and colour of the Yeelight.

#### Misc bits

Automations to determine if they're awake or asleep, if they're home, away, at work, if the phone is running low (so there can be an automated nudge to charge it) and other pieces.

### Person Two

#### Bedhead light

Turn on the bedhead light with the alarm, and turn it off half an hour later

#### Up early

Getting up early probably means a taxi ride to the airport, so turn on the number sign so the taxi driver can find the house.

#### At (the) station

Send a "will be home in X minutes", based on the travel time sensor, and taking into account the usual delays in getting from the station to the car park, and out of the car park.

#### Coming home

If they're at the station, and the other adult isn't home, notify them

#### Not working away

Uses the calendar component to turn off the the travelling boolean (this one can almost certainly go as control of the boolean is also handled elsewhere)

#### Returning

When they reach either of the local airports or major train stations, turn off the travelling boolean if they're currently travelling.

#### Travelling

When they're at least 3 hours away, turn the travelling boolean on.

#### Working away

When the calender says they're working away, set and unset various booleans (the most important being don't notify about commute delays)

#### Working from home

If the calendar says they're working from home, don't notify about commute delays

#### Working trains

If the relevant booleans are set, notify about the state of the commute

#### Misc

Standard awake, asleep, home and away toggles

### Person Three

Standard awake, home, and away toggles.

One automation to notify person2 (if they're at home) that person3 is nearly home.

## Playing music

When person2 is working from home, play music in the home office.

## Printer

Notifications when the state of one of the printers consumables gets low.

## Return trains

When person2 is working from the local office, send a notification about the state of return commute near the end of the day.

## Seasons

Set the input select for the seasons, based on the date

## Sonos

Mute the TV if the Sonos starts playing, and unmute it when it stops.

## Startup

For when I restart HA during the day

## Stopping music

At the end of the day, turn off the music in the home office.

## Sunrise

Some automations may get turned off overnight, this turns them back on at sunrise

## Table light

Two minutes after the motion is last detection in the living room, if the light was turned on automatically, turn it off

## Test automations

For when I'm testing things out

Also, at 3 AM and 3 PM run *Test Network* on the Z-Wave mesh

## Train status

In the morning, just before it's time to leave, send the notifications about the commute status 

## TV 

Turn the TV off when it's bedtime, as identified by the TV being turned off between 10 PM and 4 AM

When the TV is turned on, stop the Sonos if it's playing.

## Updater

When there's an update available, send a notification. I rarely update when the release comes out though, usually waiting a day or so to ensure there's no unexpected problems.

## Utility door

No longer just the utility door, but also the patio door - I simply haven't bothered to give it a more appropriate name.

A trio of automations to turn on and off the garden lights automatically as the door opens and closes. The trick though is that the light doesn't turn off if we just open and close the door relatively quickly. 

## Wake person one

Some people are hard to get out of bed in the morning, this is for helping one such person not sleep in.

## Winter

These are for the lighting automations during winter.

## Work



## Z-Wave
