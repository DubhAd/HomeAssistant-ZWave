# Binary sensors

Components:
* [bayesian binary sensor](https://home-assistant.io/components/binary_sensor.bayesian/)
* [binary sensor](https://home-assistant.io/components/binary_sensor/)
* [template binary sensor](https://home-assistant.io/components/binary_sensor.template/)
* [trend binary sensor](https://www.home-assistant.io/components/binary_sensor.trend/)
* [workday binary sensor](https://home-assistant.io/components/binary_sensor.workday/)

A summary of the sensors, and what they're for

## Garage

I've two sensors here I'm experimenting with. They're templates to cover when one of the sensor entities gets stuck in the open state. I'm not actively using these in any automations currently.

## Garden

This is to allow me to use an input_select to control when the garden lights turn off automatically.

## Living room

A simple template sensor [as documented here](https://home-assistant.io/docs/z-wave/entities/#burglar-entity) to turn my non-binary reporting Z-Wave sensor into a binary sensor.

## Trains

Using the [UK Transport](https://home-assistant.io/components/sensor.uk_transport/) sensor to say whether the trains for the commute are running on time. Not used in any automations right now.

## Trend

Some simple trend sensors to track:
* Whether the sun is rising or setting - this is used in the lighting automations
* If the light level is generally increasing or decreasing - again used in the lighting automations

## Workday

Standard [workday sensor](https://home-assistant.io/components/binary_sensor.workday/)

## Z-Wave

Every so often the Z-Wave mesh (well, the controller) stops behaving. I've a couple of multi sensors that report in every minute or so on average. This checks to see if it's been 10 minutes since the last state change of any Z-Wave entity. If it has, then the sensor turns off and I can use that to trigger a *Test Network* and *Heal Network* to kick things back into life.
