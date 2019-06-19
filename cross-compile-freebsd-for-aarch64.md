### Get the FreeBSD Source
svnlite checkout https://svn.freebsd.org/base/releng/12.0 /usr/src

### Compile
cd /usr/src
make -j4 kernel-toolchain TARGET=aarch64
make -j4 buildkernel KERNCONF=MYKERNEL TARGET=aarch64
make installkernel KERNCONF=MYKERNEL TARGET=aarch64 DESTDIR=/some/path
