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

Each device mentioned above has its own way of controlling and uploading
content. Some of them will be described in the following chapters.

## MicroPython in Fedora

If you want to try MicroPython and learn about the differences between MicroPython and
Python, install MicroPython with a command

```
$ sudo dnf install micropython
```

and then start an interactive MicroPython session.

```
$ micropython
MicroPython v1.7 on 2016-04-20; linux version
Use Ctrl-D to exit, Ctrl-E for paste mode
>>>
```

Using MicroPython on your computer makes sense only for some basic testing
purposes, but the main goal is to control embedded devices.

## Mu - simple IDE for BBC micro:bit

Micro:bit tries to be as simple to use as possible, so its developers decided
to make their own IDE named *Mu*. *Mu* is designated for kids to
learn the basics of programming. Your device is mounted automatically in Fedora,
so you only need one click to flash your micro:bit with your new app or to
start REPL.

*Mu* is a part of Fedora, so its installation command is

```
$ sudo dnf install mu
```

and then you can run your new IDE from a terminal or from the apps menu.

```
$ mu
```

*Mu* looks like this:

<img src="/content/tech/languages/python/micropython-mu.png" width="97%">

## uFlash - CLI for flashing the micro:bit

If you prefer to use your own text editor instead of *Mu*, *uFlash* is
the right utility for you. *uFlash* is a command line tool (written
in Python) for flashing your Python scripts to Micro:bit.

To install it, type

```
$ sudo dnf install uflash
```

The next step is to flash your script to Micro:bit. Just use the path to the script as
the first parameter for `uflash`.

```
$ uflash ./hello_world.py
```

## Esptool - CLI for flashing boards with the ESP8266 chip

If you want to control your ESP8266 device using MicroPython, write MicroPython firmware into the flash memory of your device.

You can download MicroPython firmware from [the download section of its web page](http://micropython.org/download/).
Choose the latest one suitable for your device.

`esptool` is a handy CLI application that helps you flash your device. To install it, type

```
$ sudo dnf install esptool
```

With the firmware downloaded and `esptool` installed, you need to know the last
thing to connect and flash your device - the device's name. You can find it in
the result of the `dmesg` command. Use `dmesg` with `tail` to obtain the last
ten lines of the `dmesg` output.

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

You also need the rights to access your device.
You can use `sudo` before any `esptool` and `picocom` commands
mentioned below, but the preferred and more secure way is to add your regular
user account to a special system group *dialout*. To do it, type

```
$ sudo usermod -a -G dialout <username>
```

It is necessary to logout and login for this change to take effect.

Use `esptool` to flash your device. It is suggested to erase the flash
memory before writing new firmware. To do it, type the following and do not forget to replace `ttyUSB0` with the name of your device.

```
$ esptool --port /dev/ttyUSB0 erase_flash
esptool.py v1.1
Connecting...
Erasing flash (this may take a while)...
```



And now you can write MicroPython firmware to empty the flash memory. Again, do not forget to replace `ttyUSB0` with the name of your device.

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

You might need to change the name of your device and the name of the binary file with
firmware, but other parameters such as a baud-rate (connection speed) should be OK
in most cases.

## Picocom - minimal terminal emulation program

A lot of microcontrollers (like those with the ESP8266 chip) provide a serial
console for communication with the outer world. Fedora provides a
minimalistic and handy tool for connecting to it - `picocom`.

To install it, type

```
$ sudo dnf install picocom
```

To use it, type the following (and do not forget to replace `ttyUSB0` with the name of your device).

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

`-b` parameter sets the baud-rate to 115200 bps which is the connection speed.

The last line of the output (the one with `>>>`) means that MicroPython on your device
is ready to be used. If you do not see the last line, press *Enter* on your keyboard. If you still do not see the prompt, press RESET on your device.

```
>>> print('Let the connecting to IoT begins!')
Let the connecting to IoT begins!
>>>
```
