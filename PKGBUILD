# Maintainer: Wolfgang Mader <Wolfgang_Mader at brain-frog dot de>
pkgname=fdmb-git
pkgver=r0
pkgrel=4
pkgdesc="Toolbox for estimating parameters in stochastic linear systems using the EM-algorithm"
arch=('i686' 'x86_64')
url="https://github.com/ReedWood/fdmb"
license=('GPL')
depends=('intel-tbb')
makedepends=('git' 'eigen')
optdepends=()
options=()
conflicts=()
source=($pkgname::git+https://github.com/ReedWood/fdmb.git)
md5sums=('SKIP')


pkgver() {
  cd "$srcdir/$pkgname"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  # Tested for by cmake
  export BUILDING_FOR_AUR=true
  
  cd "$srcdir/$pkgname"
  cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_INSTALL_PREFIX="$pkgdir/usr" .
  make
}

package() {
  cd "$srcdir/$pkgname"
  make install
  
  cd python
  python setup.py install --prefix="$pkgdir/usr"
}
