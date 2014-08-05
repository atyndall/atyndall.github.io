---
layout: post
title: The Sensing Trifecta
category: articles
comments: true
tags: honours
---

One of the primary goals in my [research into occupancy]({% post_url 2014-07-25-beginnings %}) is to meet The Trifecta; low cost, low power consumption, easy assembly. This is proving to be a goal not easily achieved.

A paper recommended to me shows prior work in a system called [ThermoSense](http://dl.acm.org/citation.cfm?id=2528301). ThermoSense uses a [Phillips Grid-EYE](http://pewa.panasonic.com/components/built-in-sensors/infrared-array-sensors/grid-eye/), which provides an 8x8 grid of temperature measurements that when mounted on a ceiling allow the measurement of the temperature in different sections of a room, and the extrapolation of occupancy therein.

# Sensors

From the research I have done thusfar, the Grid-EYE would meet the cost requirements, with it being only around $30USD from [DigiKey](http://www.digikey.com/product-highlights/us/en/panasonic-grid-eye/2108), however, it would require the manual development of a PCB to solder it on to, which would present significant difficulty given its size.

DigiKey offers an [evaluation board](http://www.digikey.com/product-detail/en/DKSB1015A/906-1002-ND/4360804), but this board is significantly more expensive.

An alternative that could potentially be breadboarded unlike the Grid-EYE is the [MLX90620](http://www.melexis.com/Infrared-Thermometer-Sensors/Infrared-Thermometer-Sensors/FIRray16X4-Far-InfraRed-Array-776.aspx), but it is both more expensive (around $85USD) and in an inconvenient arrangement of 16x4 instead of the Grid-EYE's 8x8.

Moving out of thermal completely, some [interesting research](http://dl.acm.org/citation.cfm?id=2426687) has also been done into using ultrasonic ranging modules like the [HC-SR04](http://www.micropik.com/PDF/HCSR04.pdf), which are much cheaper, but also would require a very different design.

# Power consumption

Another concern that must be addressed is reducing the power consumption of the Raspberry Pi if it was to be used in this arrangement; a battery powered device of this nature should last at least a couple of weeks.

The [RPi website](http://www.raspberrypi.org/help/faqs/#powerReqs) suggests that the model B consumes between 700-1000mA @ 5V, which with a reasonably sized battery would lead to a very poor lifespan if left on continuously.

One possible solution to this was the [Sleepy Pi](http://spellfoundry.com/products/sleepy-pi/), which uses a low powered Arduino board acting as a sort of watchdog to sleep and wake the RPi as necessary. With such an arrangement, the RPi could wake up at relatively long intervals (5-30 minutes), make measurements, and then sleep again. The Arduino could also be programmed to wake the RPi based information gleaned from a [passive infrared sensor](http://en.wikipedia.org/wiki/Passive_infrared_sensor)

However, using the Sleepy Pi goes against the concept of the occupancy determination being accessible in a [RESTful](http://en.wikipedia.org/wiki/Representational_state_transfer) way.

In a different vein, a system could be devised in which an low powered sensor on a battery (or energy harvesting device) reported back raw measurements on an energy efficient wireless link to a wall-socket-powered RPi, which could be responsible for the interpretation and RESTful serving of this data on a powered link.

Ideally, this could be the [Mosquino](https://code.google.com/p/mosquino/), but the lack of manufacturing presents a difficulty in using that board specifically. This also brings back issues with integrating appropriate sensors (the Grid-EYE evaluation board requires USB support).

Finally, energy harvesting sensors like those provided by EnOcean could be used in conjunction with the [EnOcean Pi module](http://www.enocean.com/en/enocean-pi/) in a similar vein as the Arduino/RPi model, but with further power savings.

More research is needed.
