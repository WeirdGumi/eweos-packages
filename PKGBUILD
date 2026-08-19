# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

pkgname=typescript
pkgver=7.0.2
pkgrel=1
pkgdesc='JavaScript with syntax for types'
arch=(x86_64 aarch64 riscv64 loongarch64)
url=https://www.typescriptlang.org
license=(Apache-2.0)
depends=(musl)
makedepends=(go)
source=($pkgname-$pkgver.tar.gz::https://github.com/microsoft/$pkgname-go/archive/refs/tags/$pkgname/v$pkgver.zip)
sha256sums=(46dff50c261aa04e23d78fb4e8b0084aa3d9ef037bba6f036da3631821836dc2)

prepare() {
  go -C $pkgname-go-$pkgname-v$pkgver mod download
}

build() {
  go -C $pkgname-go-$pkgname-v$pkgver build ./cmd/tsgo
}

package() {
  cd $pkgname-go-$pkgname-v$pkgver
  install -Dt "$pkgdir"/usr/bin tsgo
  _install_license_ LICENSE
}
