# OpenSSL

## Prerequisites
```
* A toolchain compatible with the target architecture and operating system.
```

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Download
```
$ wget https://github.com/openssl/openssl/archive/OpenSSL_1_1_1g.tar.gz
```

## Extract
```
$ tar xzf OpenSSL_1_1_1g.tar.gz 
cd openssl-OpenSSL_1_1_1g
```

## Build
Substitute *linux-armv4* with an OpenSSL os/compiler option that suits your target.
```
$ mkdir build
$ cd build
$ ../Configure linux-armv4 --cross-compile-prefix="${TARGET}-" --prefix="${STATIC_ROOT}" -no-shared -static
$ make
$ ${TARGET}-strip apps/openssl
$ make install_sw
```
