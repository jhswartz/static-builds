# libevent

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
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.12-stable/libevent-2.1.12-stable.tar.gz 
```

## Extract
```
$ tar xzf libevent-2.1.12-stable.tar.gz
$ cd libevent-2.1.12-stable
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --disable-openssl \
  CFLAGS="-I${STATIC_ROOT}/include" LDFLAGS="-static -L${STATIC_ROOT}/lib"
$ make
$ make install-strip
```
