# socat

## Prerequisites
* A toolchain compatible with the target architecture and operating system.
* OpenSSL static libraries cross-compiled for the target, if you require SSL/TLS support.

## Download
Substitute *1.7.3.4* with the latest release.
```
$ wget http://www.dest-unreach.org/socat/download/socat-1.7.3.4.tar.gz
```

## Extract
```
$ tar xzf socat-1.7.3.4.tar.gz
$ cd socat-1.7.3.4
```

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host=${TARGET} LDFLAGS="-static"
$ make
```

## Strip
```
$ ${TARGET}-strip filan procan socat 
```
