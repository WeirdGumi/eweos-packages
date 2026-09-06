# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

pkgname=xsimd
pkgver=14.3.0
pkgrel=1
pkgdesc='C++ wrappers for SIMD intrinsics'
arch=(any)
url=https://xsimd.readthedocs.io
license=(BSD-3-Clause)
makedepends=(cmake)
source=($pkgname-$pkgver.tar.gz::https://github.com/xtensor-stack/$pkgname/archive/refs/tags/$pkgver.tar.gz)
sha256sums=(b3d50e7a73fbf4642ceef30131c93414901d69eee41c2a5302db650b03e2c792)

build() {
  cmake -S $pkgname-$pkgver -B build -D CMAKE_INSTALL_PREFIX=/usr
}

package() {
  DESTDIR="$pkgdir" cmake --install build
  _install_license_ $pkgname-$pkgver/LICENSE
}
