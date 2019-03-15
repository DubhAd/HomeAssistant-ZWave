# Notifiers

Components:
* [LaMetric component](https://home-assistant.io/components/notify.lametric/)
* [Pushover](https://home-assistant.io/components/notify.pushover/)
* [REST](https://www.home-assistant.io/components/notify.rest/)
* [Slack](https://home-assistant.io/components/notify.slack/)

## Adults

This is a simple group notifier, for things that I want to ensure somebody is aware of 

## Garage

This is for when we leave the garage doors open, a mass broadcast so we remember to close the thing

## LaMetric

Three notifiers using the [LaMetric component](https://home-assistant.io/components/notify.lametric/) with different default sounds and cycles, and one using the [lmnotify package](https://github.com/keans/lmnotify) via a command line.

When I first got my [LaMetric device](https://lametric.com/) there wasn't a component, hence the command line notifier. Then a bug turned up in the component, where it would lose the auth, so I kept using it. Now, the component is reliable, and I don't need it any more... but I'm keeping it just in case.

## Logfile

Sometimes it's been useful to spit things out to logs so I can see what's happening, I keep this around for that.

## People

Individual notifiers for different methods for different people. I'm using a combination of Pushover and REST currently.

## REST

For use with Discord, since I'm using Discord anyway. This will replace Slack, and probably Pushover

## Slack

Slack is being phased out
