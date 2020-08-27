# gptfdisk 

## Prerequisites
* A toolchain compatible with the target architecture and operating system.
* libuuid from [e2fsprogs](e2fsprogs.md)

## Prepare
Substitute *arm-linux-gnueabihf* with your toolchain's target triplet.
```
$ export TARGET=arm-linux-gnueabihf
$ export STATIC_ROOT=`readlink -f ~/${TARGET}-static`
```

## Download
```
$ wget -O gptfdisk-1.0.5.tar.gz https://sourceforge.net/projects/gptfdisk/files/gptfdisk/1.0.5/gptfdisk-1.0.5.tar.gz/download 
```

## Extract
```
$ tar xzf gptfdisk-1.0.5.tar.gz
$ cd gptfdisk-1.0.5
```

## Build
```
$ CXX="${TARGET}-g++" CXXFLAGS="-I${STATIC_ROOT}/include" LDFLAGS="-static -L${STATIC_ROOT}/lib" make gdisk fixparts
$ ${TARGET}-strip gdisk fixparts
```
