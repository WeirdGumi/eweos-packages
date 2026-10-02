# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

pkgname=unrar
pkgver=7.3.1
pkgrel=1
pkgdesc='The RAR uncompression program'
arch=(x86_64 aarch64 riscv64 loongarch64)
url=https://www.rarlab.com/rar_add.htm
license=(UnRAR)
depends=(llvm-libs musl)
# 0001: From downstream. Respect CXXFLAGS and LDFLAGS.
source=(
  https://www.rarlab.com/rar/${pkgname}src-$pkgver.tar.gz
  0001-respect-cxxflags-and-ldflags.patch
)
sha256sums=(
  634900842a3737d9cc15bbcc71d4c74cc713437e0bca296a573424fe5f2660ab
  4962cf2e32a46749fe05ebe1ce496631fb1a5d83fb4a313019fc1cdc44dc4844
)

prepare() {
  _patch_ $pkgname
}

build() {
  echo $CXXFLAGS
  echo $LDFLAGS
  make -C $pkgname
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir"/usr install
  _install_license_ license.txt
}
