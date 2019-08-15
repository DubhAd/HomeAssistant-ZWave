# Change in progress

You'll note that many files have the DISABLED extension. Yes, they've been disabled _in this instance_. I'm doing
a [live migration between instances](https://blog.ceard.tech/2019/08/my-great-migration-part-one.html), mostly moving to a VM. However, I can't move everything since I'm using a 
Z-Wave GPIO hat. As a result my Pi is using [MQTT statestream](https://www.home-assistant.io/components/mqtt_statestream) to send
the details of the Z-Wave switches and sensors to my VM instance. I'm then using the [REST API](https://developers.home-assistant.io/docs/en/external_api_rest.html)
to allow that VM instance to control the Pi instance.

For the time being I'm only pushing the config of the Pi instance to Git. Once this transition completes (which
could be weeks away) I'll spin up a separate Git repo for the Pi, and this one will be updated from the VM.

# Automations, automations everywhere, and all the brains did hurt

Documentation: [automation](https://home-assistant.io/docs/automation/)

_Some of these were first written when I started with HA, and didn't know better. You'll find that I've used hyphens (-) in some file names and underscores (\_) to match Home Assistant in others. Mostly I'm not renaming files._

Most of these have been split into sub-folders, except for these

### bedtime.yaml

Sets the input boolean called `bedtime` when everybody's asleep.

### house_awake.yaml

Clears the input boolean called `bedtime` when somebody wakes up.

### printer_low.yaml

We have a laser printer, since we print so little that an inkjet is always clogging. This warns us when it starts to run low.

---

### all_away_media_off.yaml

This hasn't ever been enabled, but the idea is that if we've left home, and it's not in guest mode, this would turn off any media players left on

