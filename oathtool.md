# oathtool 

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
$ wget https://download.savannah.nongnu.org/releases/oath-toolkit/oath-toolkit-2.6.7.tar.gz
```

## Extract
```
$ tar xzf oath-toolkit-2.6.7.tar.gz
$ cd oath-toolkit-2.6.7
```

## Patch
```
$ sed -i -e 's/^\t\$(AM_LDFLAGS) \$(LDFLAGS) -o \$@/& -all-static/g' \
      oathtool/Makefile.in
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --enable-static \
  CFLAGS="-I${STATIC_ROOT}/include" LDFLAGS="-static -L${STATIC_ROOT}/lib"
$ make
$ make install-strip
```
