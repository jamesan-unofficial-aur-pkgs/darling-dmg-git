# Maintainer: James An <james@jamesan.ca>

pkgname=darling-dmg-git
_pkgname=${pkgname%-git}
pkgver=1.0.4.r1.gb7ce87b
pkgrel=1
pkgdesc="FUSE module for .dmg files (containing an HFS+ filesystem)"
arch=('i686' 'x86_64')
url="http://www.darlinghq.org"
license=('GPL3')
depends=('bzip2' 'fuse' 'icu' 'libxml2' 'openssl')
makedepends=('cmake' 'git')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
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

build() {
    cd $_pkgname

    mkdir -p build && cd build
    cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr ..
    make
}

package() {
    cd "$_pkgname/build"

    make DESTDIR="$pkgdir/" install
}
