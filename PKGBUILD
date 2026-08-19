# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

pkgname=pnpm
pkgver=11.22.0
pkgrel=1
pkgdesc='Fast, disk space efficient package manager'
arch=(any)
url=https://pnpm.io
license=(MIT)
depends=(nodejs)
makedepends=(pnpm typescript yq)
source=($pkgname-$pkgver.tar.gz::https://github.com/pnpm/pnpm/archive/refs/tags/v$pkgver.tar.gz)
sha256sums=(f70f38585ab120668702f08c63c302df9eab60124e96681f7b84f6d70eb10955)

prepare() {
  cd $pkgname-$pkgver
  yq -i '
    .scripts.compile-only |= sub("pnx node@runtime:[^ ]+", "node") |
    del(.devDependencies.@typescript/native-preview, .packageManager, .devEngines)
  ' package.json
  yq -i '
    .allowBuilds.msgpackr-extract = false
  ' pnpm-workspace.yaml
  yq -i '
    .scripts.bundle |= sub("pnx node@runtime:[^ ]+", "node")
  ' ${pkgname}11/$pkgname/package.json
  pnpm install
}

build() {
  cd $pkgname-$pkgver
  pnpm compile-only
}

package() {
  install -d "$pkgdir"/usr/bin
  ln -s /usr/lib/node_modules/$pkgname/bin/$pkgname.mjs "$pkgdir"/usr/bin/$pkgname
  ln -s /usr/lib/node_modules/$pkgname/bin/$pkgname.mjs "$pkgdir"/usr/bin/pn
  ln -s /usr/lib/node_modules/$pkgname/bin/pnpx.mjs "$pkgdir"/usr/bin/pnpx
  ln -s /usr/lib/node_modules/$pkgname/bin/pnpx.mjs "$pkgdir"/usr/bin/pnx

  cd $pkgname-$pkgver/${pkgname}11/$pkgname
  install -Dm644 -t "$pkgdir"/usr/lib/node_modules/$pkgname package.json
  install -Dt "$pkgdir"/usr/lib/node_modules/$pkgname/bin bin/*
  _install_license_ LICENSE

  cd dist
  install -Dm644 -t "$pkgdir"/usr/lib/node_modules/$pkgname/dist $pkgname.mjs pnpmrc worker.js
  install -Dm644 -t "$pkgdir"/usr/lib/node_modules/$pkgname/dist/templates templates/*
}
