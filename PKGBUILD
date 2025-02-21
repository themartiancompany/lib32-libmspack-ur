# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: AndyRTR <andyrtr@archlinux.org>

_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "GNU/Linux" ]]; then
  _compiler_libs="gcc-multilib"
  _libc="glibc"
elif [[ "${_os}" == "Android" ]]; then
  _compiler_libs="libcompiler-rt"
  _libc="ndk-sysroot"
fi
_git="true"
_ml="lib32-"
_pkg=libmspack
pkgname="${_ml}${_pkg}"
epoch=1
pkgver=1.11
_commit="305907723a4e7ab2018e58040059ffb5e77db837"
pkgrel=1
pkgdesc='A library for Microsoft compression formats'
url="https://www.cabextract.org.uk/${_pkg}/"
arch=(
  'x86_64'
  'aarch64'
)
license=(
  'GPL'
)
depends=(
  "${_ml}${_libc}"
)
makedepends=(
  "${_compiler_libs}"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    'git'
  )
fi
provides=(
  'libmspack.so'
  "${_pkg}=${pkgver}"
)
_http="https://github.com"
_ns="kyz"
_url="${_http}/${_ns}/${_pkg}"
_tag_name="commit"
_tag="${_commit}"
source=(
  "git+${_url}#${_tag_name}=${_tag}"
)
sha256sums=(
  '8772ea127d0e09f6ae60e7780634fbf0467e26fa0dc429bc207395b0117c447a'
)

pkgver() {
  cd \
    "${_pkg}"
  git \
    describe \
      --tags | \
    sed \
      's/^v//;s/[^-]*-g/r&/;s/-/+/g'
}

_usr_get() {
  local \
    _bin
  _bin="$( \
    dirname \
      "$(command \
           -v \
	   "env")")"
  dirname \
    "${_bin}"
}

prepare() {
  cd \
    "${_pkg}/${_pkg}"
  autoreconf \
    -vfi
}

build() {
  local \
    _configure_opts=() \
    _cc \
    _cxx \
    _gcc_opts=() \
    _pkg_config_path
  _pkg_config_path="${_lib}/pkgconfig"
  _gcc_opts=(
    -m32
  )
  _cc="gcc ${_gcc_opts[*]}"
  _cxx="g++ ${_gcc_opts[*]}"
  _configure_opts+=(
    --prefix="/usr"
    --sysconfdir="/etc"
    --localstatedir="/var"
    --disable-static
  )
  cd "${_pkg}/${_pkg}"
  export \
    CC="${_cc}" \
    CXX="${_cxx}" \
    PKG_CONFIG_PATH="${_pkg_config_path}"
  ./configure \
    "${_configure_opts[@]}"
  sed \
    -i \
    -e \
      's/ -shared / -Wl,-O1,--as-needed\0/g' \
    "libtool"
  make
}

check() {
  cd \
    "${_pkg}/${_pkg}"
  make \
    check
}

package() {
  local \
    _lib
  _lib="$( \
    _usr_get)/lib32"
  cd \
    "${_pkg}/${_pkg}"
  make \
    DESTDIR="${pkgdir}" \
    libdir="${_lib}" \
    install
  rm \
    -rf \
    "${pkgdir}/usr/include"
}

# vim:set sw=2 sts=-1 et:
