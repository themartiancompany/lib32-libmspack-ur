# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: AndyRTR <andyrtr@archlinux.org>

pkgname=libmspack
epoch=1
pkgver=0.11alpha
pkgrel=1
pkgdesc='A library for Microsoft compression formats'
url='https://www.cabextract.org.uk/libmspack/'
arch=('x86_64')
license=('GPL')
depends=('glibc')
makedepends=('git')
provides=('libmspack.so')
source=("git+https://github.com/kyz/libmspack#tag=tags/v${pkgver}")
sha256sums=('729d08d273ddc374fb0a72c4ab3630efbd24dc3e5a80a1374dfef05096b15812')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/^v//;s/[^-]*-g/r&/;s/-/+/g'
}

prepare() {
  cd $pkgname/$pkgname
  autoreconf -vfi
}

build() {
  cd $pkgname/$pkgname
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --disable-static
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

check() {
  cd $pkgname/$pkgname
  make check
}

package() {
  cd $pkgname/$pkgname
  make DESTDIR="$pkgdir" install
}

# vim:set sw=2 sts=-1 et:
