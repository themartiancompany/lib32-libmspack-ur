# Maintainer: AndyRTR <andyrtr@archlinux.org>

pkgname=libmspack
pkgver=0.3alpha
pkgrel=1
pkgdesc="A library for Microsoft compression formats"
arch=('i686' 'x86_64')
url="http://www.cabextract.org.uk/libmspack/"
license=('GPL')
depends=('glibc')
makedepends=()
options=('!libtool')
source=(http://www.cabextract.org.uk/libmspack/$pkgname-$pkgver.tar.gz)
md5sums=('08d08455b6d58ea649b35febd23f6386')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  ./configure --prefix=/usr --disable-static
  make
}

check() {
  cd "$srcdir/$pkgname-$pkgver"
  make check
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir/" install
}
