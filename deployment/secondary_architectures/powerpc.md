---
title: PowerPC
subsection: secondary_architectures

order: 2
---

# PowerPC
[PowerPC](https://en.wikipedia.org/wiki/PowerPC) is 32 or 64 bit instruction set architetcure and mainly used in video game consoles and embedded applications. From Fedora 22, support for 32 bit PowerPC machines have been dropped and only 64 bit machines are supported.

## Endianness
PowerPC supports both little and big endian modes and can even switch from one mode to the other at run-time. In Fedora, Power5 and newer 64 bit machines are supported in big endianness mode and are commonly referred as ppc64. In little endian mode, 64 bit Power8 machines are supported and referred as ppc64le.

## Building your application for PowerPC

To initiate a build for PowerPC, use ppc-koji command:

```
ppc-koji --scratch build rawhide srpm_pkg1
```

The above command will start a scratch build of package srpm_pkg1 against Fedora rawhide for ppc64 and ppc64le architectures. Use "ppc-koji \-\-help" in console to see all available options.

To build against other Fedora branches (e.g. F23, F24), specify specific branch name to ppc-koji in argument:

```
ppc-koji --scratch build F24 srpm_pkg1
```

If the application is only meant to run on PowerPC, specify ExclusiveArch tag in [RPM spec file](https://fedoraproject.org/wiki/How_to_create_an_RPM_package#Creating_a_SPEC_file).

```
ExclusiveArch:  ppc64 ppc64le
```

## Example

In Secondary Architectures section, we saw how to get/create iprutils srpm as an example. Now, you already have srpm (src.rpm) file of iprutils.
The following example will demonstrate how to build an application for PowerPC architecture from srpm:

```
# Initiate iprutils package build for PowerPC architecture
$ ppc-koji build --scratch rawhide iprutils-2.4.11.1-1.fc25.src.rpm
  Created task: 3298139
  Task info: http://ppc.koji.fedoraproject.org/koji/taskinfo?taskID=3298139
  ....

```
For each build, a Task ID is created in ppc koji. You can see build status and it's log by going to the url provided in Task info.

## Viewing koji builds

Builds specific to ppc64(le) are hosted at [http://ppc.koji.fedoraproject.org/](http://ppc.koji.fedoraproject.org/). UI is very similar to [primary koji](http://koji.fedoraproject.org/).


## Reaching out for help
If you face any difficulty reach out to us for help:

- On libera IRC channel [#fedora-ppc](https://web.libera.chat/?channels=#fedora-ppc)
- Send an email to <ppc@lists.fedoraproject.org> mailing list
- Get [ppc64(le) machine access](https://fedoraproject.org/wiki/Architectures/PowerPC#PPC_Shell_access_for_debugging)

## More documentation

- More Fedora PowerPC specific details cane be found at [fedoraproject wiki](https://fedoraproject.org/wiki/Architectures/PowerPC)



