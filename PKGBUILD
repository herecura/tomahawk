# Maintainer: Kuba Serafinowski <zizzfizzix(at)gmail(dot)com>
# https://github.com/zizzfizzix/pkgbuilds

pkgname=tomahawk
pkgver=0.8.2
pkgrel=2
pkgdesc="A Music Player App written in C++/Qt"
arch=('i686' 'x86_64')
url="http://tomahawk-player.org/"
license=('GPL3')
depends=('phonon-qt4' 'taglib' 'boost' 'lucene++' 'libechonest2' 'jreen' 'qtweetlib' 'quazip' 'attica-qt4' 'qtwebkit' 'liblastfm' 'sparsehash' 'qtkeychain-qt4' 'websocketpp')
makedepends=('cmake')
provides=('tomahawk')
conflicts=('tomahawk-git')
source=("http://download.tomahawk-player.org/${pkgname}-${pkgver}.tar.bz2")

install=tomahawk.install

prepare() {
  [[ -e build ]] && rm -rf build
  mkdir build

  # shared lib fix/hack
  sed '/CMAKE_SHARED_LINKER_FLAGS/d' -i "$pkgname-$pkgver"/CMakeLists.txt
  sed '/CMAKE_SHARED_LINKER_FLAGS/d' -i "$pkgname-$pkgver"/src/libtomahawk/CMakeLists.txt
}

build() {
  cd build

  cmake -DBUILD_WITH_QT4=on \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DCMAKE_INSTALL_LIBEXECDIR=lib/${pkgname} \
        -DCMAKE_BUILD_TYPE=Release \
        ../${pkgname}-${pkgver}
  make
}

package() {
  cd build
  make DESTDIR=${pkgdir} install
}

sha256sums=('522d2ef873f8548990ac1fc736c11dd08c347687c77d63b520f55207f19db3ae')
