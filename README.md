# arm_adb
Android's adb ported to ARM with automake source structures

## Prerequisites
NOTE: Please make sure you are using navite/cross gcc/g++ >= 4.9
```bash
$ sudo apt-get install libtool automake
```
For cross-compiling:
### ARM
```bash
$ sudo apt-get install linux-libc-dev-armhf-cross libc6-armhf-cross libc6-dev-armhf-cross
```
### AARCH64
```bash
$ sudo apt-get install linux-libc-dev-arm64-cross libc6-arm64-cross libc6-dev-arm64-cross
```

## How to build and run
### Native compiling
#### Native-compile openssl
```bash
$ git clone https://github.com/qhuyduong/openssl-1.0.2l.git
$ cd openssl-1.0.2l/
$ ./Configure --prefix=/tmp/openssl os/compiler:gcc
$ make && make install
$ cd -
```

#### Native-compile arm_adb
```bash
$ git clone https://github.com/qhuyduong/arm_adb
$ cd arm_adb
$ ./configure --includedir=/tmp/openssl/include --libdir=/tmp/openssl/lib
$ make
```

### Cross-compiling
#### Cross-compile Openssl
```bash
$ git clone https://github.com/qhuyduong/openssl-1.0.2l.git
$ cd openssl-1.0.2l/
$ ./Configure --prefix=/tmp/openssl os/compiler:$TOOLCHAIN_PREFIX-gcc
$ make && make install
$ cd -
```

#### Cross-compile arm_adb
```bash
$ git clone https://github.com/qhuyduong/arm_adb
$ cd arm_adb
$ ./configure --host=$TOOLCHAIN_PREFIX --includedir=/tmp/openssl/include --libdir=/tmp/openssl/lib
$ make
```

## Troubleshooting
### 1. WARNING: 'aclocal-1.xx' is missing on your system
Run below command before configure
```bash
$ autoreconf -i --force
```

## support AMB and openssl 1.1.0 
Run below command before configure
```bash
$ export LDFLAGS="-lz -L/amb/prebuild/oss/armv8-a/zlib/usr/lib -L/amb/prebuild/oss/armv8-a/openssl/usr/lib" 
$ ./configure --host=aarch64-linux-gnu --includedir=/amb/prebuild/oss/armv8-a/openssl/include
$ make
$ aarch64-linux-gnu-strip src/adb
```


