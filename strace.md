# strace

## Prerequisites
* A toolchain compatible with the target architecture and operating system.

## Download
Substitute *v5.6* with the latest release.
```
$ wget https://github.com/strace/strace/releases/download/v5.6/strace-5.6.tar.xz
```

## Extract
```
$ tar -xJvf strace-5.6.tar.xz
$ cd strace-5.6
```

## Initialise Environment
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export CFLAGS="-static -pthread"
$ export CC=${TARGET}-gcc
$ export STRIP=${TARGET}-strip
```

## Build
```
$ ./configure --host=${TARGET}
$ make
$ ${STRIP} strace
$ ls -ahl strace
-rwxr-xr-x 1 user user 1.2M May 10 18:40 strace
```