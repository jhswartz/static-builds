# zlib

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
$ wget https://zlib.net/zlib-1.2.11.tar.gz
```

## Extract
```
$ tar xzf zlib-1.2.11.tar.gz 
$ cd zlib-1.2.11
```

## Build
```
$ mkdir build
$ cd build
$ prefix="${STATIC_ROOT}" CC="${TARGET}-gcc" CFLAGS="-I${STATIC_ROOT}/include" \
  LDFLAGS="-L${STATIC_ROOT}/lib" ../configure --static
$ make
$ make install
```
