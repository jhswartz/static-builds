# gdb

## Prerequisites
* A toolchain compatible with the target architecture and operating system.

## Download
Substitute *9.1* with the latest release.
```
$ wget http://ftp.gnu.org/gnu/gdb/gdb-9.1.tar.xz
```

## Extract
```
tar xJf gdb-9.1.tar.xz
cd gdb-9.1
```

## Patch
```
$ sed -i -e 's/$MISSING makeinfo/true/g' configure
$ sed -i -e "s/RDYNAMIC=['\"].*['\"]/RDYNAMIC=''/g" gdb/{,gdbserver/}configure
$ sed -i -e 's/^CC_LD.*$/& -static/g' gdb/{,gdbserver/}Makefile.in
```

## Prepare 
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --disable-sim
$ make
$ ${TARGET}-strip gdb/{gdb,gdbserver/{gdbreplay,gdbserver}}
$ make install
```
