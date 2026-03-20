# Maintainer: Bennett Piater <bennett at piater dot name>
pkgname=zsd
pkgver=1.3.0
pkgrel=1
pkgdesc="CLI tool to find older versions of a file in ZFS snapshots"
arch=('x86_64' 'aarch64')
url="https://j-keck.github.io/zsd"
license=('MIT')
depends=('zfs-utils')
makedepends=('go')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/j-keck/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
b2sums=('739b8daa251f69f7f39b4c1d2f15ad8f3cfa6e505be7b3aeb6a5944db2c1a1576c743a6786eb68d13d99ddc661b9666ec1a1b13d01e45892e3fe67a11419c598')

prepare() {
    cd "${pkgname}-${pkgver}"
    mkdir -p build/
}

build() {
    cd "${pkgname}-${pkgver}"
    export CGO_CPPFLAGS="${CPPFLAGS}"
    export CGO_CFLAGS="${CFLAGS}"
    export CGO_CXXFLAGS="${CXXFLAGS}"
    export CGO_LDFLAGS="${LDFLAGS}"
    export GOFLAGS="-buildmode=pie -mod=readonly -modcacherw"
    go build \
        -trimpath \
        -ldflags "-compressdwarf=false -linkmode external" \
        -o build/zsd .
}

check() {
    cd "${pkgname}-${pkgver}"
    go test ./...
}

package() {
    cd "${pkgname}-${pkgver}"
    install -Dm755 build/zsd "${pkgdir}/usr/bin/zsd"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
