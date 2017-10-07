# Robot Programming
> Lab materials for how to program with Pepper by Choregraphe.<br>
> Venue: Room 4221, Teaching Lab 1, Academic Building.<br>
> Date: Nov. 3 & 10, 2017

[![Choregraphe][chor-image]][chor-url]
[![Python][py-image]][py-url]
[![naoqi][qi-image]][qi-url]
[![License][license-image]][license-url]
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com)

<!-- [![Inline docs](http://inch-ci.org/github/sunzhida/COMP4461_2017Fall_Lab2.svg?branch=master)](http://inch-ci.org/github/sunzhida/COMP4461_2017Fall_Lab2) -->
<!-- [![Build Status][travis-image]][travis-url] -->

In this lab, we will introduce how to program with [Pepper](https://www.ald.softbankrobotics.com/en/robots/pepper) robot by Choregraphe. This lab will be divided into two sessions. For the first session, we will show how to program with Choregraphe. We are going to teach programming with python in the second session. In this repository, there is a demo created by Choregraphe for you to get started.

## Table of contents

- [Overview](#overview)
- [Configuration](#configuration)
- [Development](#development)
- [Tips](#tips)
- [Contribute](#contribute)
- [Meta](#meta)

## Overview

### What is Pepper?

[Pepper](https://en.wikipedia.org/wiki/Pepper_(robot)) is a humanoid robot by Aldebaran Robotics and SoftBank designed with the ability to read emotions. The [official website](http://doc.aldebaran.com/2-4/family/pepper_technical/index_pep.html) provides a technical overview of Pepper and you can find out its structure as well as the other technical details from the instruction. You can also refer to an
<img src="./images/PEPPERbrochure_EN.pdf" alt="official brochure"  width="100%"> to obtain more general information. During the experiment, you can interact with Pepper through [contact and tactile sensors](http://doc.aldebaran.com/2-4/family/pepper_technical/contact-sensors_pep.html).

![](images/imagePepperSpec_EN.jpg)

### What is Choregraphe?

[Choregraphe](https://developer.softbankrobotics.com/us-en/downloads/pepper) is a multi-platform development application with graphical user interface. It allows you to create animations and behaviors on Pepper, test them on a simulated robot or directly on a real one, monitor and control Pepper, etc.

## Configuration

### How to install Choregraphe 2.5.5?
First, we need to prepare all the components as mentioned above. Make sure that:
* The application connects the local network created by the Wi-Fi router.
* The Wi-Fi router connects the Internet.
* The bridge connects the Wi-Fi router, and all the blue lights are on without blinking.

Note that your application and the bridge should be in the same local network.

### How to get the bridge details?
You can acquire the detail information about the bridge through [this](https://account.meethue.com/login), like the Internal IP Address, Gateway, etc. You need this information to debug with the lights when you develop your applications.

## Development

### Mobile demo
[Philips Hue](https://itunes.apple.com/us/app/philips-hue/id1055281310?mt=8) (by Philips Lighting BV) is a mobile application that lets you easily control your lights from any device and create the right ambience for every moment.

### Web demo
[Harmony for Philips Hue](http://benknight.github.io/hue-harmony/) is an open sourced web application that sets Philips Hue lights colors based on the color relationships.

### Live Demo
We will follow the tutorials [here](https://developers.meethue.com/documentation/getting-started) to show how to get familiar with the programming environments with Hue.

First, we need to obtain the _Internal IP Address_ and bridge assigned _Username_. After get connected with Hue bulb(s) via your devices, we can acquire all the bulbs' state through the link:

```
http://<Internal IP Address>/api/<Username>/lights
```

The structure of the data is like (here we use only one bulb):

```json
{
	"1": {
		"state": {
			"on": true,
			"bri": 254,
			"hue": 14910,
			"sat": 144,
			"effect": "none",
			"xy": [0.4596, 0.4105],
			"ct": 370,
			"alert": "none",
			"colormode": "ct",
			"reachable": true
		},
		"swupdate": {
			"state": "transferring",
			"lastinstall": null
		},
		"type": "Extended color light",
		"name": "Hue color lamp 1",
		"modelid": "LCT007",
		"manufacturername": "Philips",
		"uniqueid": "(omit)",
		"swversion": "5.38.1.14919"
	}
}
```

Then we can try to modify the bulb's state via:

```
http://<Internal IP Address>/api/<Username>/lights/1/state
```

with ``PUT`` method.

Note that the range for ``bri`` and ``sat`` are from ``0`` to ``254``, and the range for ``hue`` is from ``0`` to ``65535``. The bulbs we used are in ``LCT007`` model and the CIE color space is in [Gamut B](https://developers.meethue.com/documentation/core-concepts#color_gets_more_complicated).

### About the framework

This framework is built upon HTML5 Boilerplate V6.0.1, Boostrap v4 and jsHue v2.1.1. After extract the content into your server (e.g. Apache), you can get the bridge _IP Address_ from `console`.

The console information will also tell you the current state. If you get `error` message then you need to press the button on the bridge, otherwise you will receive a string generated by bridge as your _Username_. Copy the _Username_ to your local JavaScript code and save it in the `user` variable.

```js
var user = bridge.user("<your username>");
```
You will take the variable as a key to communicate with Hue.

After that you can follow the [instruction of jsHue](https://github.com/blargoner/jshue) to pass your commands to the bridge through your devices.

## Tips

- [SoftBank Robotics Documentation](http://doc.aldebaran.com/)
- test

+ Involve in the development community to get inspired, e.g., [Hue Pro Development Community](https://plus.google.com/communities/117365177082293877496).
+ Philips Hue [API](https://developers.meethue.com/philips-hue-api).
+ Philips Hue Python RGB / CIE1931 "xy" [Converter](https://github.com/benknight/hue-python-rgb-converter).
+ You can learn from the other developers’ works from [here](https://developers.meethue.com/tools-and-sdks).


## Contribute

We would love you for the contribution to **Lab2**, check the ``LICENSE`` file for more information.

## Meta

[Zhida Sun](http://zsunaj.student.ust.hk/). Distributed under the MIT license. See ``LICENSE`` for more information.

[chor-image]:https://img.shields.io/badge/Choregraphe-2.5.5-008C96.svg
[chor-url]: https://developer.softbankrobotics.com/us-en/downloads/pepper
[py-image]:https://img.shields.io/badge/Python-2.7-008C96.svg?style=flat
[py-url]: https://www.python.org/downloads/
[qi-image]:https://img.shields.io/badge/SDK-2.4.3-008C96.svg?style=flat
[qi-url]: https://community.ald.softbankrobotics.com/en/resources/software/language/en-gb/robot/pepper-3
[license-image]: https://img.shields.io/badge/License-MIT-blue.svg
[license-url]: ./LICENSE.md
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[codebeat-image]: https://codebeat.co/badges/c19b47ea-2f9d-45df-8458-b2d952fe9dad
[codebeat-url]: https://codebeat.co/projects/github-com-vsouza-awesomeios-com
