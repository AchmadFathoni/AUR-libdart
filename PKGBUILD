# Maintainer: acxz <akashpatel2008 at yahoo dot com>
# Contributor: Benjamin Chretien <chretien at lirmm dot fr>
# Contributor: Gonçalo Camelo Neves Pereira <goncalo_pereira@outlook.pt>
# Contributor: midgard <arch dot midgard "at symbol" janmaes "youknowwhat" com>
# Contributor: Zhirui Dai <daizhirui at hotmail dot com>

pkgname=libdart
pkgver=6.13.0
pkgrel=4
pkgdesc="Dynamic Animation and Robotics Toolkit"
arch=('i686' 'x86_64')
url="https://dartsim.github.io"
license=('BSD')
depends=('assimp' 'boost' 'eigen' 'fcl' 'libccd' 'bullet' 'coin-or-ipopt'
         'nlopt' 'octomap' 'ode' 'openscenegraph' 'tinyxml2' 'urdfdom'
         'glu' 'freeglut' 'libxi' 'libxmu' 'pagmo' 'fmt')
optdepends=('pagmo: pagmo optimizer support')
makedepends=('cmake')
provides=('dartsim')
_pkgname=dart
source=(
    "${pkgname}-${pkgver}.tar.gz::https://github.com/dartsim/${_pkgname}/archive/v${pkgver}.tar.gz"
    "gnu13.patch"
)
sha256sums=(
    '4da3ff8cee056252a558b05625a5ff29b21e71f2995e6d7f789abbf6261895f7'
    '1a617e94035d4e1259e795908cd76df64f5e64e35a6a8fea250fd264282ead01'
)

# Make libdart use pagmo 2.18.0 instead of 2.17.0
prepare(){
    sed -i '9s/7/8/' ${srcdir}/${_pkgname}-${pkgver}/cmake/DARTFindpagmo.cmake
    cd ${srcdir}/${_pkgname}-${pkgver}
    patch -p1 -i "${srcdir}/gnu13.patch"
}

build() {
    mkdir -p "${srcdir}/${_pkgname}-${pkgver}/build"
    cd "${srcdir}/${_pkgname}-${pkgver}/build"

    cmake .. \
        -DCMAKE_INSTALL_PREFIX="/usr" \
        -DCMAKE_INSTALL_LIBDIR="lib" \
        -DDART_TREAT_WARNINGS_AS_ERRORS="off"

    make
}

package() {
    cd "${srcdir}/${_pkgname}-${pkgver}/build"

    make DESTDIR="${pkgdir}/" install
}
