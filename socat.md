# socat

## Prerequisites
* A toolchain compatible with the target architecture and operating system.
* [OpenSSL](openssl.md) if you need TLS/SSL support.

## Download
```
$ wget http://www.dest-unreach.org/socat/download/socat-1.7.3.4.tar.gz
```

## Extract
```
$ tar xzf socat-1.7.3.4.tar.gz
$ cd socat-1.7.3.4
```

## Patch
```
$ sed -i -e 's/LIBS="$LIBS -lssl/& -lcrypto -lpthread -ldl/p' configure
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
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" \
  CFLAGS="-I${STATIC_ROOT}/include" LDFLAGS="-static -L${STATIC_ROOT}/lib"
$ make
$ make strip
$ make install
```
