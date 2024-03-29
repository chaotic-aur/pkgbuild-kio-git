# Merged with official ABS kio PKGBUILD by João, 2021/02/01 (all respective contributors apply herein)
# Maintainer: João Figueiredo & chaotic-aur <islandc0der@chaotic.cx>
# Contributor: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=kio-git
pkgver=5.83.0_r4759.g930d03d4
pkgrel=1
pkgdesc='Resource and network access abstraction'
arch=($CARCH)
url='https://community.kde.org/Frameworks'
license=(LGPL)
depends=(solid-git kjobwidgets-git kbookmarks-git libxslt kwallet-git ktextwidgets-git kded-git)
makedepends=(git extra-cmake-modules-git kdoctools-git doxygen qt5-tools)
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
optdepends=('kio-extras-git: extra protocols support (sftp, fish and more)' 'kdoctools-git: for the help kioslave'
            'kio-fuse-git: to mount remote filesystems via FUSE')
groups=(kf5-git)
source=("git+https://github.com/KDE/${pkgname%-git}.git")
sha256sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}
  _ver="$(grep -m1 'set(KF5\?_VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
  echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

build() {
  cmake -B build -S ${pkgname%-git} \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DBUILD_TESTING=OFF \
    -DBUILD_QCH=ON
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
