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

## Check
Consider removing the *-new* suffix from affected binaries.
```
$ ls -ahl binutils/{addr2line,ar,cxxfilt,elfedit,nm-new,objcopy} \
          binutils/{objdump,ranlib,readelf,size,strings,strip-new} \
          gas/as-new gprof/gprof ld/ld-new
-rwxr-xr-x 1 user user 902K May 11 17:42 binutils/addr2line
-rwxr-xr-x 1 user user 918K May 11 17:42 binutils/ar
-rwxr-xr-x 1 user user 898K May 11 17:42 binutils/cxxfilt
-rwxr-xr-x 1 user user 382K May 11 17:42 binutils/elfedit
-rwxr-xr-x 1 user user 911K May 11 17:42 binutils/nm-new
-rwxr-xr-x 1 user user 988K May 11 17:42 binutils/objcopy
-rwxr-xr-x 1 user user 1.3M May 11 17:42 binutils/objdump
-rwxr-xr-x 1 user user 918K May 11 17:42 binutils/ranlib
-rwxr-xr-x 1 user user 927K May 11 17:42 binutils/readelf
-rwxr-xr-x 1 user user 902K May 11 17:42 binutils/size
-rwxr-xr-x 1 user user 898K May 11 17:42 binutils/strings
-rwxr-xr-x 1 user user 988K May 11 17:42 binutils/strip-new
-rwxr-xr-x 1 user user 1.4M May 11 17:42 gas/as-new
-rwxr-xr-x 1 user user 947K May 11 17:42 gprof/gprof
-rwxr-xr-x 1 user user 1.6M May 11 17:42 ld/ld-new

$ file -b binutils/{addr2line,ar,cxxfilt,elfedit,nm-new,objcopy} \
          binutils/{objdump,ranlib,readelf,size,strings,strip-new} \
          gas/as-new gprof/gprof ld/ld-new
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, ...
```
