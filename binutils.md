# GNU Binary Utilities

## Prerequisites
* A toolchain compatible with the target architecture and operating system.

## Download
Substitute *2.34* with the latest release.
```
$ wget http://ftp.gnu.org/gnu/binutils/binutils-2.34.tar.xz
```

## Extract
```
tar xJf binutils-2.34.tar.xz 
cd binutils-2.34
```

## Patch
Don't apply the following if you have makeinfo and actually want the documentation installed.
```
$ cp configure{,.orig}
$ sed -i -e 's/$MISSING makeinfo/true/g' configure
```

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet, and adjust the *STATIC_ROOT* to your liking.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --disable-nls --with-stage1-ldflags="--static"
$ make
$ make install-strip
```
