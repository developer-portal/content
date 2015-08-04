---
title: C and C++
page: c
section: tech-languages
---

## C and C++ installation and usage

### C

C is a compiled language and as such it needs a compiler. To install a compiler, simply type:

```
# sudo dnf install gcc
```

This command should download and install package with compiler called gcc.
To compile a program written in C, simply run the gcc like this:

```
# gcc your_source.c
```

This will produce a binary file created from your source code. By default, this binary file is named `a.out`. 
You can run this binary by typing:

```
# ./a.out
```

There are many options which you can use when running a compiler. These are some of the basics options used with gcc:

```
# gcc -std=c11 your_source.c -o your_binary
```
The option `-std=c11` states the c11 or iso9899:2011 C language standard to be used when compiling your code. 
The `-o name` option simply states the name of the binary created by gcc.
To see all the options which you can use with gcc simply view its man page like this:

```
# man gcc
```

### C++

Like C, C++ is also a compiled language. It has many similarities with C and to some extent it is safe to say that C is
subset of C++ and C++ supports every programming technique supported by C. Next command shows how to install C++ compiler:

```
# sudo dnf install g++
```

To compile your program you can do the same as was described above with C:
```
# g++ -std=c++14 your_source.cpp -o your_binary
```
Again in the command above there are a few examples of possible options which can be used. 
`-std=c++14` states the version of standard used when compiling your code. `-o name` again states the name of your binary program. 
You can than run your program by typing:

```
# ./your_binary
```

To view all the options that g++ can use, visit the man page by typing:
```
# man g++
```
You will see that the man page is identical with the one shown for gcc.

