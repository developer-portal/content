---
title: Work with Arduino
subsection: arduino
section: start-hw
description: Using Arduino with Fedora as a workstation.
---

# Arduino platform

Arduino is a very popular hardware platform among hobbyists. [Arduino boards](https://www.arduino.cc/en/Main/Products) are usually based on AVR platform (using ATmega 8-bit microcontrollers), however there are some boards based on 32-bit ARM microcontrollers ([Arduino Due](https://www.arduino.cc/en/Main/ArduinoBoardDue)) or even boards combining ATmega AVR microcontroller with MIPS processor running Linux distribution based on OpenWRT ([Arduino Yún](https://www.arduino.cc/en/Main/ArduinoBoardYun)). Arduino boards are easy to use and ideal for hardware beginners. The microcontrollers are pre-programed with a bootloader allowing you to upload the binary firmware using only USB cable and software programmer.

You can not really run Fedora on Arduino boards, however you can easily use Fedora for developing you applications and projects for Arduino. Extensive documentation on how to write your application for Arduino, together with available libraries and language reference can be found on the [project page](https://www.arduino.cc/en/Guide/HomePage).

There are couple of possibilities how to interact with and program your Arduino board on Fedora. These are covered in the following sections.

## Arduino IDE

Arduino project has its own graphical IDE for developing projects based on Arduino boards.
It allows you to:
 * develop your code with syntax highlighting
 * browse available libraries and importing new ones
 * compile the code for specific board
 * upload the binary firmware to the board using variety of programmers
 * connect to the board's serial console and communicate with it

To install Arduino IDE on Fedora, just run:

    $ sudo dnf install arduino

Now you are all set to start developing you project using Arduino IDE on Fedora. Just start it from your desktop environment applications menu or run the <code>arduino</code> command from the command line. For more information on how to use the Arduino IDE, please refer to the [documentation](https://www.arduino.cc/en/Guide/Environment).

<!--
## Ino

In contrast to Arduino IDE, the Ino tool is only command line oriented. It is ideal if you want to develop the project source using your favorite text editor and do all the tasks from the command line. You can even script some of the tasks and run those as part of the CI if you want.

To install Ino tool on Fedora, just run:

    $ sudo dnf install ino

After the installation you will have the <code>ino</code> command available. Ino expect a specific directory structure for your project in order to work.

You can use the <code>ino init</code> command for setting up the project directory structure. This will create <code>src/</code> directory for your project sources and <code>lib/</code> directory for the libraries your project is using.

To list all supported boards use <code>ino list-models</code> command. To build the binary firmware use <code>ino build</code> with appropriate parameters. For uploading the compiled sketch use <code>ino upload</code> command and to communicate with your board using serial console use <code>ino serial</code> command.

For more information about the project and supported options, please refer to the [documentation](http://inotool.org/) or use the <code>-h</code> option after the specific command.
-->

<!--
## Platform IO

Add this section once platform-io is packaged for Fedora

http://platformio.org/
-->
