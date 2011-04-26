# Maintainer: AndyRTR <andyrtr@archlinux.org>

pkgname=libmspack
pkgver=0.2alpha
pkgrel=1
pkgdesc="A library for Microsoft compression formats"
arch=('i686' 'x86_64')
url="http://www.cabextract.org.uk/libmspack/"
license=('GPL')
depends=('glibc')
makedepends=()
options=('!libtool')
source=(http://www.cabextract.org.uk/libmspack/$pkgname-$pkgver.tar.gz)
md5sums=('a51c65ba1dc9b53090d4e65e1f55d860')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir/" install
}
