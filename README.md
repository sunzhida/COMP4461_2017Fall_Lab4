# Robot Programming
> Lab materials for how to program Pepper with Python.<br>
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

According to the official [website](http://doc.aldebaran.com/2-5/dev/tools/naoqi.html), NAOqi is the main software running on the robot. Without NAOqi, the robot cannot perform any behaviors. NAOqi can run on the robot under NAOqi OS distribution, and can also run on your computer in order to test the code on a simulated robot. [Here](http://doc.aldebaran.com/2-5/dev/programming_index.html) is an overview of all the SDKs.

## Configuration

### How to install Python?

Before we get started, we need to install Python package on the local machine.

#### Linux & MAC

For Linux users, you can directly run

```bash
sudo apt-get install python-2.7 python-pip
```

. Otherwise, you may refer to this [link](https://askubuntu.com/questions/101591/how-do-i-install-the-latest-python-2-7-x-or-3-x-on-ubuntu) to see how to install the latest Python by downloading the install package from the official website.

For Mac users, you can install python by running:

```bash
brew install python
```

to install the latest version of Python 2.7.x.

#### Windows

First, you need to install Python on your laptop. Please download the ``.msi`` file from [here](https://www.python.org/downloads/). Then install the package in `C:\Python27`. You may change the path according to your situations.
After installing the Python package, please go to
`My Computer > Properties > Advanced System Settings > Environment Variables`. Under `System variables`, find `Path` and click the `edit` button, in the popped out window, add your path (e.g., `C:\Python27`) of Python directory in the last line.
After the installation, you can check the current version of your Python environment by typing

```
python --version
```

in CMD. If the feedback is Python `2.7.XX`, then you can go to the next step.

### How to install NAOqi SDK?

You need a SoftBank Robotics account to get all the installer that you need. Create your account [here](https://sso.aldebaran-robotics.com/pf/adapter2adapter.ping?TargetResource=https://cloud.aldebaran-robotics.com/). After you create the account, sign in and go to this [page](https://community.ald.softbankrobotics.com/en/resources/software/language/en-gb).
Please find the __Pepper SDKs and documentation 2.5.5__ and download the corresponding SDK based on your operating system.

#### Linux & MAC

For Linux, please download [Python 2.7 SDK 2.5.5 Linux 64](https://community.ald.softbankrobotics.com/en/resources/software/pepper-sdks-and-documentation-255); and for Mac, please download [Python 2.7 SDK 2.5.5 Mac 64](https://community.ald.softbankrobotics.com/en/resources/software/pepper-sdks-and-documentation-255).

In Linux, please go to the folder where you download the file (e.g., ``~/Downloads``) and unzip the ``.tar.gz`` file by

```bash
tar -xvzf pynaoqi-python2.7-2.5.5.5-linux64.tar.gz
```

Then move the folder to your local library by the following command (if you get `Permission denied`, please add `sudo` at the beginning of this line of command).

```bash
mv -i ./pynaoqi-python2.7-2.5.5.5-linux64 /usr/local/lib/pynaoqi
```

By doing this, we rename the unzipped folder as `pynaoqi` and move it in our local environment. Next, go to ``/usr/local/lib/pynaoqi``, then follow the instruction [here](http://doc.aldebaran.com/2-5/dev/python/install_guide.html)
to set up your local environment. Now your ``/path/to/python-sdk/lib/python2.7/site-packages`` should be ``/usr/local/lib/pynaoqi/lib/python2.7/site-packages``
Then type

```bash
export PYTHONPATH=${PYTHONPATH}:/usr/local/lib/pynaoqi/lib/python2.7/site-packages
```

, after that you can start to code in this environment.

However, you will find the path is invalid after you finish the current session or close the dialog window. Please add the last command at the end of your ``.bashrc`` file. In this way, you can get the working environment after restarting the terminal.

If you are using MAC, you need to do the same as for the Ubuntu users. Besides, please add the following additional line after the last `PYTHONPATH` setting command:

```bash
export DYLD_LIBRARY_PATH=${DYLD_LIBRARY_PATH}::/usr/local/lib/pynaoqi/lib
```

#### Windows

For Windows, please download [Python 2.7 SDK 2.5.5 Win 32 Binaries](https://community.ald.softbankrobotics.com/en/resources/software/pepper-sdks-and-documentation-255), and unzip the file into `C:\pynaoqi`. Then go to `My Computer > Properties > Advanced System Settings > Environment Variables` again, and under `System variables`, add a new user variable `PYTHONPATH` and set it as the `path\to\python-sdk\lib` (e.g., `C:\pynaoqi\lib`).

For other installation information, you can refer to [here](http://doc.aldebaran.com/2-5/dev/python/install_guide.html#python-install-guide).

## Implementation

After setting up the environment, you can type in the following code to test your environment setup:

```python
from naoqi import ALProxy
tts = ALProxy("ALTextToSpeech", "<IP of your robot>", 9559)
tts.say("Hello, world!")
```

If the Pepper speaks ``Hello, world!``, then you have set up the development environment successfully. We will announce the IP address during the class. If you forget the IP when you experiment, please press pepper’s Chest button, and it will say it.

There is a demo code provided in this repository for you to get aware how to call NAOqi APIs in python. This demo aims to detect human faces and tell their genders and expressions from what has been detected. After changing the IP address of the robot, you can run this code by simply typing

```bash
python expression_teller.py
```

in python environment. There are also plenty of demos offered on the official documentation website.

## Tips

- Note that you have to find the right version of the [SoftBank Robotics Documentation](http://doc.aldebaran.com/) with your local NAOqi development environment.
- [Configure & setting](http://doc.aldebaran.com/2-5/nao/webpage.html).
- Get started with [NAOqi](http://doc.aldebaran.com/2-5/dev/community_software.html#retrieving-software).

## Contribute

We would love you for the contribution to **Lab4**, check the ``LICENSE`` file for more information.

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
