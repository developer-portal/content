---
label: Command Line Application

title: Command Line Application
subsection: cli-app
section: start-sw
description: Creating a command line application using C
---

# Command Line Application

Creating command line apps using various programming languages is easy with Fedora. For this example we will write a simple c program that gathers system info and prints to stdout.

## Getting started

### Install required libraries

For simple C programs a compiler and a text editor is all we need to get started.

For this example we will use [`gcc`](https://gcc.gnu.org/) as our compiler.

```$ sudo dnf install gcc```

### Create a workspace

```$ mkdir work && cd work```

## Command Line Application in C

For this example we will use the uname function in [utsname](http://pubs.opengroup.org/onlinepubs/7908799/xsh/sysutsname.h.html) C library to gather information about the system similar to the output of the `uname -a` command and format it into a human readable block.  

The output from our example cli should match the output of `uname` with the corresponding switches. 

Here is an example of the `uname` output we are trying to achieve using `cat` to match the format

```
$ cat << EOF
Node Info
---------- 
node: $(uname -n)          
system: $(uname -s)
version: $(uname -v)
release: $(uname -r)
arch: $(uname -m)

EOF
```

The results look like this

```
Node Info
----------
node: fedora
system: Linux
version: #1 SMP Tue Sep 4 15:56:14 UTC 2018
release: 4.18.5-200.fc28.x86_64
arch: x86_64
```

## Write code for command line application


Our example is a simple one file C program. To get started we need to write our C code into a file named `nodeinfo.c`

You can write the C file using the editor of your choice.

```$ gedit nodeinfo.c```

Here is the example code for `nodeinfo.c`

```c
// Node Info Cli App
#include <sys/utsname.h>
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

int main()
{
    // define utsname struct
    struct utsname info;
    // call uname() and check call
    if (uname(&info) < 0)
    {
        // error if call fails
        perror("uname");
        fprintf(stderr, "Error in uname : %d\n", errno);
        exit(EXIT_FAILURE);
    } else {
        // Print Node Info
        printf("Node Info\n----------\n");
        printf("node : %s\n", info.nodename);
        printf("system : %s\n", info.sysname);
        printf("version : %s\n", info.version);
        printf("release : %s\n", info.release);
        printf("arch : %s\n", info.machine);
        exit(EXIT_SUCCESS);
    }
}


```

Save the file as `nodeinfo.c`.

## Compile code for command line application

We can compile our cli at the command line using `gcc`. To do this open a terminal and navigate to your workspace. 

The command is as follows.

```$ gcc -o nodeinfo nodeinfo.c```

The `gcc` command flag `-o nodeinfo` tells `gcc` to generate a binary named `nodeinfo` in the same directory as `nodeinfo.c`. 

The binary should be executable so give it a spin.

```$ ./nodeinfo```

And the output should be similar to this

```
Node Info
----------
node : fedora
system : Linux
version : #1 SMP Tue Sep 4 15:56:14 UTC 2018
release : 4.18.5-200.fc28.x86_64
arch : x86_64
```



## Source Code

Source code for this and more examples

[https://github.com/xbcsmith/cli-app](https://github.com/xbcsmith/cli-app)


