# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

_name=scipy
pkgname=python-$_name
pkgver=1.18.1
pkgrel=1
pkgdesc='An open-source software for mathematics, science, and engineering'
arch=(x86_64 aarch64 riscv64 loongarch64)
url=https://scipy.org
license=(BSD-3-Clause)
depends=(python)
makedepends=(cython meson-python pybind11 python-build python-numpy python-pythran)
checkdepends=()
source=($pkgname-$pkgver.tar.gz::https://github.com/$_name/$_name/archive/refs/tags/v$pkgver.tar.gz)
sha256sums=(dc0bd51a213c2e26e93f6182105d55aa3e065dde9a84db8e4044afbc5103c50b)

build() {
  cd $_name-$pkgver
  python -m build -wn
}

check() {
  cmake -S $_name-$pkgver -B build ${cmake_vars[@]/#/-D}
  make -C build check
}

package() {
  cd $_name-$pkgver
  python -m installer -d "$pkgdir" dist/*.whl

  local sitepkgs=$(python -c 'import sysconfig; print(sysconfig.get_path("purelib"))')
  install -d "$pkgdir"/usr/share/licenses
  ln -s $sitepkgs/$_name-$pkgver.dist-info/licenses/LICENSE "$pkgdir"/usr/share/licenses/$pkgname
}
