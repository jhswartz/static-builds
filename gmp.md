# gmp 

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
$ wget https://ftp.gnu.org/gnu/gmp/gmp-6.2.1.tar.xz
```

## Extract
```
$ tar xJf gmp-6.2.1.tar.xz
$ cd gmp-6.2.1
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" \
  --disable-shared --enable-static=yes --with-pic
$ make
$ make check
$ make install-strip
```
