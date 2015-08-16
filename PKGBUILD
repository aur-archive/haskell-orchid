# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=orchid
pkgname=haskell-orchid
pkgver=0.0.8
pkgrel=4
pkgdesc="Haskell Wiki Library"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:BSD3')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-quickcheck=2.1.1.1' 'haskell-bytestring=0.9.1.7' 'haskell-containers' 'haskell-encoding<0.6' 'haskell-extensible-exceptions=0.1.1.1' 'haskell-fclabels<0.2' 'haskell-filestore<0.3' 'hscolour<1.12' 'haskell-mtl<1.2' 'haskell-nano-md5<0.2' 'haskell-parsec' 'haskell-process=1.0.1.3' 'haskell-salvia<0.2' 'haskell-salvia-extras<0.2' 'haskell-stm=2.1.2.1' 'haskell-time=1.1.4' 'haskell-unix' 'haskell-xml<1.4')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
md5sums=('67f265cd4989752c5ad47914ce1dab18')
