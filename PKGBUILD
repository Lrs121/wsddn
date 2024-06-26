# Maintainer: Larson Thorpe <ltthorpe@lrsservers.org>
pkgname=wsddn
_altname=wsdd-native
pkgver=1.12
pkgrel=1
pkgdesc="C++ implementation of WS-Descovery daemon influenced by wsdd and wsdd2"
arch=('x86_64' 'armv7h' 'aarch64')
license=('BSD-3-Clause')
url="https://github.com/gershnik/wsdd-native"
makedepends=('clang' 'cmake' 'git')
conflicts=('wsdd' 'wsdd2' 'wsdd-git' 'wsdd2-git' 'wsdd-bin' 'wsdd2-bin')
backup=('etc/conf.d/wsddn.conf')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
    "wsddn.service"
    "wsddn.conf"
    "wsddn.sysusers"
)

b2sums=('9ad5a154fdb6d72ebea0f819146a07c3746c7b7f41505bc9e0977b63889a4ce4368cec74467e3d7b9f18d010793060258d7f17738f506b2f8451d466a47bc4e2'
        '6d897529bdd90c9d2258568f880d4a8180bb39f26cb40dead105d253ba87c1394291f618d8873908bb7db887fa4ddaab31d7a7b1f13485fc1b1cea5c40b40643'
        'ec5ada0067634a019da056600e34c42b8c0ce465e66850f12087b75967fc69f4a2d1b9f04f1b16afeeaf83aaa1e5af18d9f8408b726b273e214181f5d95a4394'
        'c0086f18df123e08a3bd18a8d1bbdb158f30533f13f455867cdf64c229d8e880a40b10bdee619b36b557cdd37a094270c175a020c4fe4123bf0c24c433050206')

build() {
    cd "${_altname}-${pkgver}/"

    # Doesnt build with system libxml2 keep PREFER_SYSTEM set to OFF
    cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
        -DCMAKE_INSTALL_PREFIX="/usr" \
        -DFETCHCONTENT_QUIET=OFF \
        -DWSDDN_PREFER_SYSTEM=ON \
        -DWSDDN_WITH_SYSTEMD="yes" \
        -Bbuild -S.

    cmake --build build
}

package() {
    cd "${_altname}-${pkgver}/build"

    DESTDIR="${pkgdir}" cmake --install .

    cd "${srcdir}"
    install -Dm644 wsddn.service "${pkgdir}/usr/lib/systemd/system/wsddn.service"
    install -Dm644 wsddn.conf "${pkgdir}/etc/conf.d/wsddn.conf"
    install -Dm644 wsddn.sysusers "${pkgdir}/usr/lib/sysusers.d/wsddn.conf"
}
