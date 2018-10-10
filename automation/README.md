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

### tv-off-bedtime.yaml

Triggered by:

* The TV being off for 5 minutes
* The utility door closing

Requires:

* The TV to be off
* It to be between 22:00 and 04:00

This has effectively been replaced by the room specific automations.

---

### moved_to_family_room.yaml

This is an old automation that used to handle us moving to the family room while the living room lights were on. Now handled by the living_room_away automation.

### adults_home_lights_on.yaml

This is an old automation that's been disabled. Rather than blindly turning on all the lights when we arrive, that's handled on a room by room basis now.

### all-away-lights-off.yaml

This is an old automation that's been disabled. Rather than blindly turning off all the lights when we leave, that's handled on a room by room basis now.

### all_away_media_off.yaml

This hasn't ever been enabled, but the idea is that if we've left home, and it's not in guest mode, this would turn off any media players left on

