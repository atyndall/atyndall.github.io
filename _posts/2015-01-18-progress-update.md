---
layout: post
title: January progress update
category: articles
comments: true
tags: honours
---

In the last few weeks I've been really getting into the meat of the project; the circuit has been designed and implemented (see Figure 1) and [fairly stable software](https://github.com/atyndall/thing/blob/e9724a30d10fc663a281fe82fd36f850c8118c00/node/mlx90620_driver/mlx90620_driver.ino) has been developed for the Arduino to allow it to send the temperature information to the connected computer.

A [Python library](https://github.com/atyndall/thing/tree/4dfbbee61a46ee16ec59960c54e37212f8100dbf/coordinator/processing/thinglib) for the parsing, analysis, recording and visualisation of the sensor data has been developed; currently unimaginatively named "thinglib". You can part of the visualisation in operation in Figure 2. Hopefully it'll get a better name when the project does.

<figure>
	<a href="/images/posts/2015-01-18-progress-update/mlx-arduino-circuit.png"><img src="/images/posts/2015-01-18-progress-update/mlx-arduino-circuit.png"></a>
	<figcaption><a href="/images/posts/2015-01-18-progress-update/mlx-arduino-circuit.png" title="MLX Arduino Circuit">Figure 1: MLX Arduino Circuit</a></figcaption>
</figure>

The above circuit diagram was developed from the actual breadboard connections, and hopefully is an accurate representation of how that all plugs together.

<figure>
	<a href="/images/posts/2015-01-18-progress-update/system-1-full.jpg"><img src="/images/posts/2015-01-18-progress-update/system-1-small.jpg"></a>
	<figcaption><a href="/images/posts/2015-01-18-progress-update/system-1-full.jpg" title="Whole System">Figure 2: Whole System</a><br><br>
	a) "thinglib" temperature visualisation<br>
	b) Raspberry Pi with built-in camera<br>
	c) Sensor circuit
	</figcaption>
</figure>

To allow for the simultaneous capture of visual and thermal data, I've stuck the sensor and a Raspberry Pi to the same piece of board, close enough hopefully to eliminate most FOV issues.

<figure>
	<a href="/images/posts/2015-01-18-progress-update/system-2-full.jpg"><img src="/images/posts/2015-01-18-progress-update/system-2-small.jpg"></a>
	<figcaption><a href="/images/posts/2015-01-18-progress-update/system-2-full.jpg" title="Circuit Closeup">Figure 2: Circuit Closeup</a><br><br>
	a) Sensor itself<br>
	b) I2C level shifter<br>
	c) Arduino Uno R3
	</figcaption>
</figure>

In the current design the sensor sends the calculated raw temperature over serial to a computer where "thinglib" parses it and visualizes it.


<figure>
	<iframe width="560" height="315" src="//www.youtube.com/embed/uCtErT1JISk" frameborder="0" allowfullscreen></iframe>
	<figcaption>Figure 3: First Sensor Test</figcaption>
</figure>

This is the first test I did of capturing both the thermal data from the sensor and the visual data from the Pi, then overlaying the two. They're not overlayed correctly, and it goes pretty badly out of sync at the end, but it'll be a useful debugging tool.

<figure>
	<iframe width="560" height="315" src="//www.youtube.com/embed/NmK1knOOhck" frameborder="0" allowfullscreen></iframe>
	<figcaption>Figure 4: Deviation Code Test</figcaption>
</figure>

This is a test using a cup of hot water of the standard deviation calculation code which is used to separate the "thermal background" from the image, so that analysis can be performed on the image results. Currently the extraction of the feature vectors required for the classifier techniques is complete, so now the question is to implement the classifiers.

Much is left to do.