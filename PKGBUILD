# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

pkgname=c3-lsp
pkgver=0.4.0
pkgrel=1
pkgdesc='Language Server for the C3 language'
arch=(x86_64 aarch64 riscv64 loongarch64)
url=https://pherrymason.github.io/c3-lsp
license=(GPL-3.0-only)
depends=(musl)
makedepends=(go)
source=($pkgname-$pkgver.tar.gz::https://github.com/pherrymason/$pkgname/archive/refs/tags/v$pkgver.tar.gz)
sha256sums=(0709fbe44c5bcbbfa26bd4f06acde81948b89e36e8152fe937a10fe2dea3dbb2)

prepare() {
  go mod download -C $pkgname-$pkgver/server
}

build() {
  make -C $pkgname-$pkgver build
}

check() {
  make -C $pkgname-$pkgver test
}

package() {
  cd $pkgname-$pkgver
  install -Dt "$pkgdir/usr/bin" server/bin/c3lsp
  _install_license_ LICENSE
}
