# Maintainer: AndyRTR <andyrtr@archlinux.org>

pkgname=libmspack
pkgver=1.5
pkgrel=1
pkgdesc="A library for Microsoft compression formats"
arch=('x86_64')
url="http://www.cabextract.org.uk/libmspack/"
license=('GPL')
depends=('glibc')
source=(#http://www.cabextract.org.uk/libmspack/$pkgname-$pkgver.tar.gz
        https://github.com/kyz/libmspack/archive/v${pkgver}.tar.gz)
sha256sums=('a5383c4d662b6148f368327bfee2babed2436d5395654ea71e491a8eb6a6f947')

prepare(){
  cd $pkgname-$pkgver/$pkgname/trunk
  autoreconf -vfi
}

build() {
  cd $pkgname-$pkgver/$pkgname/trunk
  ./configure --prefix=/usr --disable-static
  make
}

check() {
  cd $pkgname-$pkgver/$pkgname/trunk
  make check
}

package() {
  cd $pkgname-$pkgver/$pkgname/trunk
  make DESTDIR="$pkgdir/" install
}
