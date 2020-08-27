# e2fsprogs

## Prerequisites
* A toolchain compatible with the target architecture and operating system.

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Download
```
$ wget -O e2fsprogs-1.45.6.tar.gz https://sourceforge.net/projects/e2fsprogs/files/e2fsprogs/v1.45.6/e2fsprogs-1.45.6.tar.gz/download 
```

## Extract
```
$ tar xzf e2fsprogs-1.45.6.tar.gz
$ cd e2fsprogs-1.45.6
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --enable-libuuid LDFLAGS="-static"
$ make
$ make install-strip
```

If libuuid is required elsewhere (eg. gptfdisk):
```
$ cd lib/uuid
$ make install
```
