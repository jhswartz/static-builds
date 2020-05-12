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

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host=${TARGET} --disable-nls --with-stage1-ldflags="--static"
$ make MAKEINFO=true
```

## Strip
```
$ ${TARGET}-strip binutils/{addr2line,ar,cxxfilt,elfedit,nm-new,objcopy} \
                  binutils/{objdump,ranlib,readelf,size,strings,strip-new} \
                  gas/as-new gprof/gprof ld/ld-new
```
