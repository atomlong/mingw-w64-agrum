pkgname=mingw-w64-agrum
pkgver=0.16.1
pkgrel=1
pkgdesc="C++ Bayesian networks library (mingw-w64)"
license=('LGPL')
arch=('any')
url="http://agrum.gitlab.io/"
depends=('mingw-w64-crt')
makedepends=('mingw-w64-cmake')
options=('!buildflags' 'staticlibs' '!strip')
source=("https://gitlab.com/agrumery/aGrUM/-/archive/${pkgver}/aGrUM-${pkgver}.tar.bz2")
sha256sums=('a1204b5d995d5404e1cc67911ed907aab90f2971bd50f495711f39196dc1a014')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

prepare () {
  cd aGrUM-$pkgver
}

build() {
  cd aGrUM-$pkgver
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-cmake -DBUILD_PYTHON=OFF ..
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "$srcdir/aGrUM-${pkgver}/build-${_arch}"
    make install DESTDIR="$pkgdir"
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}

