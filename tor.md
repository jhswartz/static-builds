# tor 

## Prerequisites
* A toolchain compatible with the target architecture and operating system.
* [libevent](libevent.md)
* [OpenSSL](openssl.md)
* [zlib](zlib.md)

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Download
```
$ wget https://dist.torproject.org/tor-0.4.4.6.tar.gz
```

## Extract
```
$ tar xzf tor-0.4.4.6.tar.gz
$ cd tor-0.4.4.6
```

## Patch
```
$ sed -i -e 's/LIBS="\$tor_saved_LIBS -lssl -lcrypto/LIBS="-lssl -lcrypto $tor_saved_LIBS/g' \
         -e 's/LIBS="\$LIBS -lssl -lcrypto/LIBS="-lssl -lcrypto $LIBS/g' \
         -e 's/AR cru/AR cr/g' configure
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" \
  --disable-tool-name-check --enable-static-tor \
  --with-openssl-dir="${STATIC_ROOT}/lib" --with-zlib-dir="${STATIC_ROOT}/lib" \
  --with-libevent-dir="${STATIC_ROOT}/lib" CFLAGS="-I${STATIC_ROOT}/include" \
  LDFLAGS="-L${STATIC_ROOT}/lib"
$ make
$ make install-strip
```
