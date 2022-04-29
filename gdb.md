# gdb

## Prerequisites
* A toolchain compatible with the target architecture and operating system,
  capable of C and C++ compilation.
* [gmp](gmp.md)

## Prepare 
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Download
```
$ wget http://ftp.gnu.org/gnu/gdb/gdb-11.2.tar.xz
```

## Extract
```
tar xJf gdb-11.2.tar.xz
cd gdb-11.2
```

## Patch
```
$ sed -i -e 's/$MISSING makeinfo/true/g' configure
$ sed -i -e "s/RDYNAMIC=['\"].*['\"]/RDYNAMIC=''/g" {gdb,gdbserver}/configure
$ sed -i -e 's/^CC_LD.*$/& -static/g' {gdb,gdbserver}/Makefile.in

# If you receive SIGABRT immediately after executing gdb:
$ sed -i -e 's/n_worker_threads = -1/n_worker_threads = 0/g' gdb/maint.c
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" --disable-sim
$ make
$ ${TARGET}-strip gdb/gdb gdbserver/{gdbreplay,gdbserver}
$ make install
```
