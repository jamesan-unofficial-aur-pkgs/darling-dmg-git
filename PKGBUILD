# Maintainer: James An <james@jamesan.ca>

pkgname=darling-dmg-git
_pkgname=${pkgname%-git}
pkgver=1.0.4.r1.gb7ce87b
pkgrel=1
pkgdesc="FUSE module for .dmg files (containing an HFS+ filesystem)"
arch=('i686' 'x86_64')
url="http://www.darlinghq.org"
license=('GPL3')
depends=('fuse' 'icu' 'libxml2')
makedepends=('git' 'boost')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
options=()
install=
source=("$_pkgname"::"git+https://github.com/darlinghq/$_pkgname.git")
md5sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  (
    set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g;s/^v//' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

prepare() {
  cd "$_pkgname"

  [ -d build ] \
    && find build -mindepth 1 -delete \
    || mkdir build
}

build() {
    cd "$_pkgname/build"

    cmake -DWITH_TESTS=1 -DCMAKE_INSTALL_PREFIX=/usr ..
    make
}

check() {
    cd "$_pkgname/build"

    make -k test
}

package() {
    cd "$_pkgname/build"

    make DESTDIR="$pkgdir/" install
}
