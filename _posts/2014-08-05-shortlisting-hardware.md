---
layout: post
title: Shortlisting Hardware
category: articles
comments: true
tags: honours
---

I'm learning rapidly that the area of occupancy is booming at the moment, and the set of possible options for sensors and host hardware is of considerable size.

To help trim down my list to a set of viable and non-viable candidates, I've needed to come up with a more stringent set of criteria, and measure possible solutions against them.

# Criteria
The set of criteria I am attempting to optimise for are:

* **Cost**; the set of components required should aim to minimise cost, as these devices are intended to be deployed in situations where the user may not have much money.

* **Invasiveness**; the sensors used in the system should gather as little information as necessary to achieve the detection goal; there are privacy concerns with the use of high-definition sensors.

* **Energy Efficiency**; the system may be placed in a situation where there is no access to mains power, so ability to survive for long periods on only battery power is advantageous.

* **Reliability**; the system should be able to operate without user intervention or frequent maintenance, and should be able to perform its multi-occupant detection goal with a high degree of accuracy.

# Host options
There are are a variety of options for configurations that can host the sensor:

* **Raspberry Pi (battery)**: A Raspberry Pi with a set of sensors connected to it operates on a rechargeable battery pack.

* **Raspberry Pi & Sleepy Pi (battery)**: A Raspberry Pi with the [Sleepy Pi](http://spellfoundry.com/products/sleepy-pi/) addon operates on a wake-sleep cycle with a set of sensors connected to it.

* **Arduino (battery)**: An Arduino board with a set of sensors connected operates on a rechargeable battery pack, with on board data processing.

* **Raspberry Pi (mains), Arduino (battery)**: An Arduino board with a set of sensors connected operates on a rechargeable battery pack. A Raspberry Pi communicates with it and handles the data processing aspect.

* **TMote Sky (battery)**: A MoteIV Tmote Sky, the same as that used in the ThermoSense paper. {% cite beltran2013thermosense %}


# Sensor options
There are similarly a variety of sensors that can either be used directly, or act as proxies for occupancy in a given area.

* **Thermal Array**: A thermal array is used to measure temperatures in different sections of a room. The use of them to detect occupancy is covered in multiple papers. {% cite erickson2013thermosense %}, {% cite erickson2013toss %}

* **Tagging**: By assuming occupants have smartphones, it is possible to use them as a proxy for occupancy. {% cite kleiminger2013using %}

* **Ultrasonic**: Through the use of ultrasonic measurement of distance, passage through doorways can be directionally measured. {% cite hnat2012doorjamb %}

* **Power Consumption**: By assuming occupants will switch on electronic devices when they enter a room, broad power consumption can act as a proxy for occupancy. {% cite kleiminger2013occupancy %}

* **Network traffic**: By assuming occupants will use computers when they enter a room, network traffic can act as a proxy for occupancy. {% cite ting2013occupancy %}

* **Cameras**: Computer Vision algorithms can be used on video and images to determine the number of people present in the scene. {% cite erickson2013poem %}

* **Fusion**: Multiple different solutions can be combined to help optimise over multiple criteria. {% cite yang2012multi %}


# Comparison

| Host | Cost | Energy Efficiency |
|:-|:-:|:-:|:-:|
| RPi | $50 | 1000mA |
| RPi & SleepyPi | $105 | dependent |
| Arduino Yun | $70 | 500MA |
| Arduino Uno  | $125 | 50mA |
| TMote Sky | $105 | 25mA |

Cost includes that of compatible 802.11 adaptor if it doesn't have built in wireless capabilities.


| Sensor | Type | Cost | Invasiveness | Reliability |
|:-|:-:|:-:|:-:|:-:|
| Grid-Eye | Thermal | $30 | Low | High |
| 802.11 card | Tagging | $15 | Low | Medium |
| HC-SR04 | Ultrasonic | $5 | Low | Low |
| OV7670 | Camera (Arduino) | $10 | High | Low |
| OV5647 | Camera (RPi) | $40 | High | High |

I'll be evaluating these options over the next week.

# References
{% bibliography --cited %}


