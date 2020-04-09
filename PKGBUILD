pkgname=riseup-vpn
pkgver() {
   cd "${pkgname}_package"
   git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
pkgrel=1
pkgdesc="RiseupVPN is a branded build of Bitmask VPN. Bitmask VPN is a minimal rewrite of the Bitmask VPN Client, written in golang, that for now lacks client authentication, and is preconfigured to use a single provider."
arch=('x86_64')
url="https://0xacab.org/leap/riseup-vpn_package"
license=('GPL3')
depends=(
    'gtk3'
    'libappindicator-gtk3'
    'python'
    'openvpn'
)
makedepends=(
    'go'
    'git'
    'pkgconf'
)
source=(
    "git+https://0xacab.org/leap/riseup-vpn_package.git"
)
sha1sums=(
    'SKIP'
)
build() {
    cd "${pkgname}_package"
    go get -u golang.org/x/text/cmd/gotext github.com/cratonica/2goarray
    make get
    make build
}

package() {
    cd "${pkgname}_package"
    install -Dm755 helpers/bitmask-root "${pkgdir}/usr/bin/bitmask-root"
    install -D helpers/se.leap.bitmask.policy "${pkgdir}/usr/share/polkit-1/actions/se.leap.bitmask.policy"
    install -Dm755 build/bin/bitmask-vpn "${pkgdir}/usr/bin/$pkgname"
    install -D debian/riseup-vpn.desktop "${pkgdir}/usr/share/applications/${pkgname}.desktop"
    install -D debian/icons/scalable/riseupvpn.svg "${pkgdir}/usr/share/icons/hicolor/scalable/apps/riseupvpn.svg"
}
