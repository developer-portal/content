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

Each device mentioned above has its own way for controlling it and uploading
content to it. In next chapters we describe some of them.

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
the right utility for you. *uFlash* is a simple command line tool (written
in Python) for flashing your Python scripts to Micro:bit.

Installation is simple as before:

```
$ sudo dnf install uflash
```

Next step is to flash your script to Micro:bit. Just use path to script as
first parameter for `uflash`.

```
$ uflash ./hello_world.py
```

## Esptool - CLI for flashing boards with the ESP8266 chip

If you want to control your ESP8266 device using MicroPython, first of all, you
will need to write MicroPython firmware into the flash memory of your device.

You can download MicroPython firmware from [the download section of its web page](http://micropython.org/download/).
Choose the latest one suitable for your device.

`esptool` is handy CLI application which helps you to flash your device. Let's
install it:

```
$ sudo dnf install esptool
```

With firmware downloaded and `esptool` installed you need to know the last
thing to connect and flash your device - device name. You can find it in
the result of `dmesg` command. Use `dmesg` with `tail` to obtain only last
ten lines of `dmesg` output:

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

The name of your device starts with *tty*.

Yes, you know the name of your device, but you also need rights to access it.
You can use `sudo`, of course, before any `esptool` and `picocom` commands
mentioned below, but preferred and more secure way is to add your regular
user account to special system group *dialout*. Use this simple command
to do it:

```
$ sudo usermod -a -G dialout <username>
```

Is necessary to logout and login for this change to take effect.

Now you can use `esptool` to flash your device. Is suggested to erase flash
memory before writing new firmware. Let's do it.

```
$ esptool --port /dev/ttyUSB0 erase_flash
esptool.py v1.1
Connecting...
Erasing flash (this may take a while)...
```

It is obvious that you need to change `ttyUSB0` to name of your device.

And now you can write MicroPython firmware to empty flash memory.

```
$ esptool --port /dev/ttyUSB0 --baud 115200 write_flash --flash_size=8m 0 esp8266-20160909-v1.8.4.bin 
esptool.py v1.1
Connecting...
Running Cesanta flasher stub...
Flash params set to 0x0020
Writing 565248 @ 0x0... 565248 (100 %)
Wrote 565248 bytes at 0x0 in 49.0 seconds (92.3 kbit/s)...
Leaving...
```

Maybe you will need to change device name as before and name of binary file with
firmware, but other parameters as baud-rate (connection speed) should be ok
in most cases.

## Picocom - minimal terminal emulation program

A lot of microcontrollers (like those with the ESP8266 chip) provide a serial
console for communication with the outer world. And Fedora provides a
minimalistic and handy tool for connecting to it - `picocom`.

And guess what? Yes, installation is as simple as possible:

```
$ sudo dnf install picocom
```

Usage of `picocom` is simple as well:

```
$ picocom -b 115200 /dev/ttyUSB0
picocom v1.7

port is        : /dev/ttyUSB0
flowcontrol    : none
baudrate is    : 115200
parity is      : none
databits are   : 8
escape is      : C-a
local echo is  : no
noinit is      : no
noreset is     : no
nolock is      : no
send_cmd is    : sz -vv
receive_cmd is : rz -vv
imap is        : 
omap is        : 
emap is        : crcrlf,delbs,

Terminal ready

>>>
```

`-b` parameter sets baud-rate to 115200 bps which is actually connection speed.

Yes, the last line of output with `>>>` means that MicroPython on your device
is ready to use. If you don't see the last line, press *Enter* on your
keyboard. If you still don't see the prompt, press RESET on your device.

```
>>> print('Let the connecting to IoT begins!')
Let the connecting to IoT begins!
>>>
```
