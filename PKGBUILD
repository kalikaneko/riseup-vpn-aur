pkgname=riseup-vpn-git
pkgver() {
   cd "bitmask-vpn"
   git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
pkgrel=1
pkgver=0.20.4
pkgdesc="RiseupVPN is a branded build of Bitmask VPN. Bitmask VPN is a minimal rewrite of the Bitmask VPN Client, written in golang, that for now lacks client authentication, and is preconfigured to use a single provider."
arch=('x86_64')
url="https://0xacab.org/leap/bitmask-vpn"
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
    "git+https://0xacab.org/leap/bitmask-vpn.git"
)
sha1sums=(
    'SKIP'
)
build() {
    cd "bitmask-vpn"
    make depends
    PROVIDER=riseup
    make build
}

package() {
    cd "bitmask-vpn"
    install -Dm755 helpers/bitmask-root "${pkgdir}/usr/bin/bitmask-root"
    install -D helpers/se.leap.bitmask.policy "${pkgdir}/usr/share/polkit-1/actions/se.leap.bitmask.policy"
    install -Dm755 build/bin/linux/bitmask-vpn "${pkgdir}/usr/bin/$pkgname"
}
