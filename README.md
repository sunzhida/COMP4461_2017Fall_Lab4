# Robot Programming
> Lab materials for how to program with Pepper by Python.<br>
> Venue: Room 4221, Teaching Lab 1, Academic Building.<br>
> Date: Nov. 10, 2017

[![Python][py-image]][py-url]
[![naoqi][qi-image]][qi-url]
[![License][license-image]][license-url]
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com)

In this lab, we will introduce how to program with [Pepper](https://www.ald.softbankrobotics.com/en/robots/pepper) robot by Python.

## Table of Contents

- [Overview](#overview)
- [Configuration](#configuration)
- [Implementation](#implementation)
- [Tips](#tips)
- [Contribute](#contribute)
- [Meta](#meta)

## Overview

### What is NAOqi?

According to the official [website](http://doc.aldebaran.com/2-5/dev/tools/naoqi.html), NAOqi is the main software running on the robot. Without NAOqi, the robot cannot perform any behaviors. NAOqi can run on the robot under NAOqi OS distribution, and can also run on your computer in order to test the code on a simulated robots.

## Configuration

### How to install Python?

#### MAC & Linux

#### Windows

### How to install NAOqi SDK?

You need a SoftBank Robotics account to get all the installer that you need. Create your account [here](https://sso.aldebaran-robotics.com/pf/adapter2adapter.ping?TargetResource=https://cloud.aldebaran-robotics.com/). After you create the account, sign in and go to this [page](https://community.ald.softbankrobotics.com/en/resources/software/language/en-gb).
Please find the __Pepper SDKs and documentation 2.5.5__ and download the corresponding SDK based on your operating system.

#### MAC & Linux

For Linux, please download [Python 2.7 SDK 2.5.5 Linux 64](https://community.ald.softbankrobotics.com/en/resources/software/pepper-sdks-and-documentation-255); and for Mac, please download [Python 2.7 SDK 2.5.5 Mac 64](https://community.ald.softbankrobotics.com/en/resources/software/pepper-sdks-and-documentation-255).

In Linux, please go to the folder where you download the file (e.g., ``~/Downloads``) and unzip the ``.tar.gz`` file by

```bash
tar -xvzf pynaoqi-python2.7-2.5.5.5-linux64.tar.gz
```

Move the folder to your local library by the following command (if you get “Permission denied”, please add “sudo” at the beginning of this line of command).
mv -i ./pynaoqi-python2.7-2.5.5.5-linux64 /usr/local/lib/pynaoqi
By doing this, we rename the unzipped folder as “pynaoqi” and move it in our local environment. Next, go to /usr/local/lib/pynaoqi, then follow the instruction here http://doc.aldebaran.com/2-5/dev/python/install_guide.html
to set up your local environment. Now your ‘/path/to/python-sdk/lib/python2.7/site-packages’ should be ‘/usr/local/lib/pynaoqi/lib/python2.7/site-packages’
Then type
export PYTHONPATH=${PYTHONPATH}:/usr/local/lib/pynaoqi/lib/python2.7/site-packages
You will find the path is invalid after you finish the current session or close the dialog window.
Please add the last command at the end of your .bashrc file. In this way, you can have the working environment after restarting the terminal.

If you are using MAC, you need to do the same as for the Ubuntu users. Besides, please add the following additional line after the last ‘PYTHONPATH’ setting command:
export DYLD_LIBRARY_PATH=${DYLD_LIBRARY_PATH}::/usr/local/lib/pynaoqi/lib


#### Windows

For Windows, please download [Python 2.7 SDK 2.5.5 Win 32 Binaries](https://community.ald.softbankrobotics.com/en/resources/software/pepper-sdks-and-documentation-255).

First, we need to prepare all the components as mentioned above. Make sure that:
* The application connects the local network created by the Wi-Fi router.
* The Wi-Fi router connects the Internet.
* The bridge connects the Wi-Fi router, and all the blue lights are on without blinking.

Note that your application and the bridge should be in the same local network.


## Implementation

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
[qi-image]:https://img.shields.io/badge/NAOqi-2.5.5-008C96.svg?style=flat
[qi-url]: https://community.ald.softbankrobotics.com/en/resources/software/language/en-gb/robot/pepper-3
[license-image]: https://img.shields.io/badge/License-MIT-blue.svg
[license-url]: ./LICENSE.md
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[codebeat-image]: https://codebeat.co/badges/c19b47ea-2f9d-45df-8458-b2d952fe9dad
[codebeat-url]: https://codebeat.co/projects/github-com-vsouza-awesomeios-com
