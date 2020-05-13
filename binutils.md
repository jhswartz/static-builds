# GNU Binary Utilities

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
$ wget http://ftp.gnu.org/gnu/binutils/binutils-2.34.tar.xz
```

## Extract
```
tar xJf binutils-2.34.tar.xz 
cd binutils-2.34
```

## Patch
```
$ sed -i -e 's/$MISSING makeinfo/true/g' configure
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --disable-nls --with-stage1-ldflags="--static"
$ make
$ make install-strip
```
