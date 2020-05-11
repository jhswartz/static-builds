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
Overcome non-configurable obstacles that force dynamic linkage.
```
$ cp gdb/configure{,.orig}
$ sed -i -e "s/RDYNAMIC=['\"].*['\"]/RDYNAMIC=''/g" gdb/configure

$ cp gdb/Makefile.in{,.orig}
$ sed -i -e 's/^CC_LD.*$/& -static/g' gdb/Makefile.in

$ cp gdb/gdbserver/configure{,.orig}
$ sed -i -e "s/RDYNAMIC=['\"].*['\"]/RDYNAMIC=''/g" gdb/gdbserver/configure

$ cp gdb/gdbserver/Makefile.in{,.orig}
$ sed -i -e 's/^CC_LD.*$/& -static/g' gdb/gdbserver/Makefile.in
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
$ ../configure --host=${TARGET}
$ make MAKEINFO=true
```

## Strip
```
$ ${TARGET}-strip gdb/{gdb,gdbserver/{gdbreplay,gdbserver}}
```
