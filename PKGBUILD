# Maintainer: AndyRTR <andyrtr@archlinux.org>

pkgname=libmspack
pkgver=0.0.20060920alpha
pkgrel=1
pkgdesc="A library for Microsoft compression formats"
arch=('i686' 'x86_64')
url="http://www.cabextract.org.uk/libmspack/"
license=('GPL')
depends=('glibc')
makedepends=()
options=('!libtool')
source=(http://www.cabextract.org.uk/libmspack/$pkgname-$pkgver.tar.gz)
md5sums=('72003dfa5da2e843e3d5ae0c18f7c969')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  ./configure --prefix=/usr --disable-static
  make || return 1
  make DESTDIR="$pkgdir/" install || return 1
}
