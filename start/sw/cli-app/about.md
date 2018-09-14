---
label: Command Line Application

title: Command Line Application
subsection: cli-app
section: start-sw
description: Creating a command line application using C
---

# Command Line Application

Creating command line apps using various programming languages is easy with Fedora. For this example we will write a simple c program that gathers system info and outputs it as json.

## Getting started

### Install required libraries

```sudo dnf install vim-enhanced clang make json-c-devel json-c pkgconfig```

```mkdir work && cd work```

## Write Code for command line application

Write the C file for our command line.

```vim nodeinfo.c```

Add some code to find out system information

```
// Node Info Cli App
#include <errno.h>
#include <json-c/json.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/sysinfo.h>
#include <sys/utsname.h>

int main()
{
    /* Conversion constants. */
    const long minute = 60;
    const long hour = minute * 60;
    const long day = hour * 24;
    const double megabyte = 1024 * 1024;
    float load_shift = 1.f / (1 << SI_LOAD_SHIFT);
    /* End Constants */
    struct sysinfo si; // Yes
    if (sysinfo(&si) < 0)
    {
        perror("sysinfo");
        fprintf(stderr, "Error in sysinfo : %d\n", errno);
        exit(EXIT_FAILURE);
    }
    struct utsname ni; // As in knights who say
    if (uname(&ni) < 0)
    {
        perror("uname");
        fprintf(stderr, "Error in uname : %d\n", errno);
        exit(EXIT_FAILURE);
    }
    // use json-c for output
    // Main Object
    json_object *object = json_object_new_object();
    // Node Info Object
    json_object *nodeinfo = json_object_new_object();
    json_object *nodename = json_object_new_string(ni.nodename);
    json_object *system = json_object_new_string(ni.sysname);
    json_object *version = json_object_new_string(ni.version);
    json_object *release = json_object_new_string(ni.release);
    json_object *arch = json_object_new_string(ni.machine);
    json_object_object_add(nodeinfo, "node", nodename);
    json_object_object_add(nodeinfo, "system", system);
    json_object_object_add(nodeinfo, "version", version);
    json_object_object_add(nodeinfo, "release", release);
    json_object_object_add(nodeinfo, "arch", arch);
    // Add Node Info to main object
    json_object_object_add(object, "nodeinfo", nodeinfo);
    // System Info Object
    json_object *systeminfo = json_object_new_object();
    json_object *memtotal = json_object_new_double(si.totalram / megabyte);
    json_object *memfree = json_object_new_double(si.freeram / megabyte);
    json_object *nprocs = json_object_new_double(si.procs);
    // Load Averages
    json_object *loadaverages = json_object_new_array();
    for (unsigned int i=0;i<3;i++)
    {
        json_object *load = json_object_new_double(si.loads[i] * load_shift);
        json_object_array_add(loadaverages, load);
    }
    // Calculate Uptime ... this is ugly
    json_object *uptime = json_object_new_object();
    int bufsize = 32;
    char* upstr = malloc(bufsize);
    if (snprintf(upstr, bufsize, "%ld:%02ld:%02ld",
                (si.uptime % day)/hour,
                (si.uptime % hour)/minute,
                si.uptime % minute) >= bufsize)
    {
        fprintf(stderr, "Failed to format uptime string : %d\n", errno);
        exit(EXIT_FAILURE);
    }
    json_object *up = json_object_new_string(upstr);
    json_object *days = json_object_new_double(si.uptime/day);
    json_object_object_add(uptime, "up", up);
    json_object_object_add(uptime, "days", days);
    // Add objects to systeminfo
    json_object_object_add(systeminfo, "memtotal", memtotal);
    json_object_object_add(systeminfo, "memfree", memfree);
    json_object_object_add(systeminfo, "nprocs", nprocs);
    json_object_object_add(systeminfo, "loadaverages", loadaverages);
    json_object_object_add(systeminfo, "uptime", uptime);
    // Add System Info to main object
    json_object_object_add(object,"systeminfo", systeminfo);
    // Print JSON
    printf("%s\n", json_object_to_json_string(object));
    exit(EXIT_SUCCESS);
}


```

## Compile Code for command line application

Next create a Makefile

```vim Makefile```

Add some content to the Makefile

```
CC = $(shell which clang)
CFLAGS = -Wall -lm -I'.'
CFLAGS += $(shell pkg-config --cflags json-c)
LDFLAGS += $(shell pkg-config --libs json-c)

all: nodeinfo

nodeinfo: nodeinfo.c
    $(CC) $(CFLAGS) $(LDFLAGS) $(TARGET_ARCH) -o $@ $<

install:
    install -m 0755 -d $(DESTDIR)/bin
    install -m 0755 nodeinfo $(DESTDIR)/bin/nodeinfo
    rm -f nodeinfo

clean:
    rm -f nodeinfo

.PHONY: all install clean
```

Use make to compile the command line

```make```

## Test the command line application

Test the binary output

```./nodeinfo```

Output should be information about the system (formatted for the web)

```
{
    "nodeinfo": {
        "arch": "x86_64",
        "node": "fedora",
        "release": "4.18.5-200.fc28.x86_64",
        "system": "Linux",
        "version": "#1 SMP Tue Sep 4 15:56:14 UTC 2018"
    },
    "systeminfo": {
        "loadaverages": [
            0.080078125,
            0.0166015625,
            0.00537109375
        ],
        "memfree": 15071.73046875,
        "memtotal": 16039.51953125,
        "nprocs": 201.0,
        "uptime": {
            "days": 1.0,
            "up": "4:23:00"
        }
    }
}
```

## Install Command Line Application

Now we can test the install

```make install DESTDIR=./test```

Binary should be installed as ./test/bin/nodeinfo

To install it into /usr/local use sudo and change the DESTDIR

```sudo make install DESTDIR=/usr/local```



