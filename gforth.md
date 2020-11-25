# gforth


## Prerequisites
* A toolchain compatible with the target architecture and operating system.
* QEMU user emulation and binfmt_misc, assuming cross-compilation under Linux.
* [gdb](gdb.md) if your target needs to use disasm-gdb for discode.


## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Download
```
$ wget http://ftp.gnu.org/gnu/gforth/gforth-0.7.3.tar.gz
```

## Extract
```
$ tar xzf gforth-0.7.3.tar.gz
$ cd gforth-0.7.3
```

## Build
```
$ mkdir build
$ cd build
$ ../configure --host="${TARGET}" --prefix="${STATIC_ROOT}" LDFLAGS="-static" \
  INSTALL_PROGRAM="\${INSTALL} --strip-program=${TARGET}-strip -s"
$ make
$ make install
```

## Note
Deploy *gforth.fi* and set GFORTHPATH accordingly.
