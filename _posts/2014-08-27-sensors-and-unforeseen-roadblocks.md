---
layout: post
title: Infrared sensors and unforeseen roadblocks
category: articles
comments: true
tags: honours
---

One thing that I've learned in the past few weeks is that your setbacks can emerge from nowhere, and aren't necessarily within your control, or even your field.

[Rachel](http://people.csse.uwa.edu.au/rachel/) and I agreed that the project should begin with a more general investigation of the sensor capabilities and requirements (the [reliability]({% post_url 2014-08-13-research-proposal %}#aim) criteria) before branching out into the other areas.

However when we went to order the Grid-EYE from [Digi-Key](http://www.digikey.com/product-highlights/us/en/panasonic-grid-eye/2108), one of the best contenders in the [options examined]({% post_url 2014-08-05-shortlisting-hardware %}#sensor-options) we were presented with the following message upon clicking "Add to Cart";

>Due to U.S. export controls, we are unable to add this item to your order.

*Huh?*

Confused, I emailed Digi-Key about the issue, asking if there was any way to order the sensor in Australia, and for more information about the restrictions. I got the following response;

>Hello, thank you for your inquiry.
>
>Thank you for your order.  I apologize, but due to contractual agreements with certain manufacturers; we are unable to supply you with the part .
>
>I apologize for any inconvenience this has caused you, and I look forward to doing business with you in the future.

This was very disappointing. The Grid-EYE was looking to be one of the best sensors for our purpose, and now it's become a difficult part to order. Even if we circumvented the restrictions via a colleague in the United States, using such difficult to acquire sensor would go against the goals of low-cost and easy assembly.

# The Alternative

For now, we've decided to investigate the [Melexis MLX90620](http://www.melexis.com/Infrared-Thermometer-Sensors/Infrared-Thermometer-Sensors/MLX90620-776.aspx) as a substitute, as it does not appear to have similar ordering restrictions and seems to be based on similar technologies.

The primary disadvantage of the sensor is that it is in a 16x4 array, which is far less useful for scanning a square room than the 8x8 arrangement that the Grid-EYE offers. There are videos on YouTube of people hooking the sensor up to stepper motors and rotating it on one axis to get an effective 16x16 thermal array instead. This may be an option for the project.

For now, getting it working with a RPi for testing purposes is the goal.