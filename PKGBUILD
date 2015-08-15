# Maintainer: Martin Schmölzer <mschmoelzer@gmail.com>

# Based on the summon-arm-toolchain script by Piotr Esden-Tempski
# https://github.com/esden/summon-arm-toolchain

pkgname=cross-arm-none-eabi-gdb
pkgver=7.5.1
pkgrel=3
pkgdesc="The GNU Debugger for the ARM EABI (bare-metal) target."
arch=(i686 x86_64)
url="http://www.gnu.org/software/gdb/"
license=('GPL3')
groups=('cross-arm')
depends=('ncurses' 'expat' 'python2')
makedepends=('texinfo')
optdepends=('openocd: for debugging JTAG targets')
options=(!libtool !emptydirs)
source=(ftp://ftp.gnu.org/gnu/gdb/gdb-${pkgver}.tar.bz2)
sha256sums=('070b808d289fa8f0291738eeaccc0cd7700d476998781f572856155240d29d20')

build() {
  cd ${srcdir}/gdb-${pkgver}

  sed -i "/ac_cpp=/s/\$CPPFLAGS/\$CPPFLAGS -O2/" libiberty/configure

  mkdir build
  cd build

  ../configure --target=arm-none-eabi \
               --prefix=/usr \
               --enable-multilib \
               --enable-interwork \
               --with-system-readline \
               --disable-nls
  make
}

package() {
  cd ${srcdir}/gdb-${pkgver}/build

  make DESTDIR=${pkgdir} install

  # libiberty.a conflicts with host version
  rm -f  ${pkgdir}/usr/lib/libiberty.a

  # We don't want these files in a cross version
  rm -rf ${pkgdir}/usr/share/info
  rm -rf ${pkgdir}/usr/share/gdb
  rm -rf ${pkgdir}/usr/include/gdb
}

# vim: set ts=2 sw=2 ft=sh noet:

