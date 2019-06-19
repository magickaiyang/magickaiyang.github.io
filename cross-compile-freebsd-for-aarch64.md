### Get the FreeBSD Source
```shell-script
svnlite checkout https://svn.freebsd.org/base/releng/12.0 /usr/src
```

### Customization
```shell-script
cd /usr/src
cp sys/arm64/conf/GENERIC sys/arm64/conf/MYKERNEL
```

Make the desired changes to the source and kernel config file.

### Compile and Install
```shell-script
make -j4 kernel-toolchain TARGET=arm64
make -j4 buildkernel KERNCONF=MYKERNEL TARGET=arm64
make installkernel KERNCONF=MYKERNEL TARGET=arm64 DESTDIR=/some/path
```

### Recompile after Changes
```shell-script
make clean
make -j4 buildkernel KERNCONF=MYKERNEL TARGET=arm64
```
