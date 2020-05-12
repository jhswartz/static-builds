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

## Patch
Use the target toolchain's strip command.
```
$ cp Makefile.in{,.orig}
$ sed -i -e 's/strip $(PROGS)/$(TARGET)-&/g' Makefile.in
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
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" LDFLAGS="-static"
$ make
$ make strip
$ make install
```
