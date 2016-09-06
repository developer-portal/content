---
title: MicroPython
subsection: python
order: 4
---

# MicroPython - Python for microcontrollers

[MicroPython](https://micropython.org/) is a special light
implementation of Python 3 that includes a small subset of the Python
standard library and is optimized to run on microcontrollers.

You can use MicroPython on various boards such as:
* BBC micro:bit ([webpage](https://www.microbit.co.uk/))
* Boards with the ESP8266 chip ([various boards wiki](http://www.esp8266.com/wiki/doku.php?id=esp8266-module-family))
* MicroPython pyboard ([store](https://micropython.org/store/#/store))
* WiPy ([webpage](https://www.pycom.io/solutions/py-boards/wipy/))

## MicroPython in Fedora

If you just want to try MicroPython and learn the differences between it and
its bigger brother, you can install it with this simple command

```
$ sudo dnf install micropython
```

and then you can start an interactive MicroPython session

```
$ micropython
MicroPython v1.7 on 2016-04-20; linux version
Use Ctrl-D to exit, Ctrl-E for paste mode
>>>
```

Using MicroPython on your computer makes sense only for some basic testing
purposes, but the main goal is to control embedded devices. Let's do it!

## Mu - simple IDE for BBC micro:bit

Micro:bit tries to be as simple to use as possible, so its developers decided
to make their own IDE named *mu*. *Mu* is designated for kids to
learn basics of programming. In Fedora, your device is mounted automatically,
so you only need one click to flash your micro:bit with your new app or to
start REPL.

*Mu* is part of Fedora, so its installation command is simple:

```
$ sudo dnf install mu
```

and then you can run your new IDE from a terminal or from apps menu.

```
$ mu
```

And this is how *Mu* looks like. Simple, right?

<img src="/content/tech/languages/python/micropython-mu.png" width="97%">

## uFlash - CLI for flashing the micro:bit

If you prefer to use your favorite text editor instead of *Mu*, *uFlash* is
 the right utility for you. *uFlash* is a simple command line tool (written in Python)
for flashing your Python scripts to Micro:bit.

Installation is simple as before:

```
$ sudo dnf install uflash
```

Next step is to flash your script to Micro:bit. Just use path to script as
first parameter for `uflash`.

```
$ uflash ./hello_world.py
```

## Picocom - minimal terminal emulation program

A lot of microcontrollers (like those with the ESP8266 chip) provide a serial
console for communication with the outer world. And Fedora provides a minimalistic
and handy tool for connecting to it - `picocom`.

And guess what? Yes, installation is as simple as possible:

```
$ sudo dnf install picocom
```

For connection, you first need to know device name which you want to connect to.
You can find it in the result of `dmesg` command. Use `dmesg` with `tail` to
obtain only last ten lines of `dmesg` output:

```
$ dmesg | tail
[703169.886296] ch341 1-1.1:1.0: device disconnected
[703176.972781] usb 1-1.1: new full-speed USB device number 45 using ehci-pci
[703177.059448] usb 1-1.1: New USB device found, idVendor=1a86, idProduct=7523
[703177.059454] usb 1-1.1: New USB device strings: Mfr=0, Product=2, SerialNumber=0
[703177.059457] usb 1-1.1: Product: USB2.0-Serial
[703177.060474] ch341 1-1.1:1.0: ch341-uart converter detected
[703177.062781] usb 1-1.1: ch341-uart converter now attached to **ttyUSB0**
```

The name of your device starts with *tty*. Now you can connect to your device with
picocom.

```
$ sudo picocom -b 115200 /dev/ttyUSB0
```

`sudo` may be necessary here to gain privileges to access attached device and
`-b` parameter sets baud-rate to 115200 bps which is actually connection speed.

If you don't want to use `sudo` for `picocom`, use this command to add your
regular user account to *dialout* group:

```
$ sudo usermod -a -G dialout <username>
```
