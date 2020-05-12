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
$ tar xJf strace-5.6.tar.xz
$ cd strace-5.6
```

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet, and adjust *STATIC_ROOT* if need be.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" CFLAGS="-pthread" LDFLAGS="-static"
$ make
$ make install-strip
```
