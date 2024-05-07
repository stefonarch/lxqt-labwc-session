#general for me
NAME=${PWD##*/}
FOLDER=$(pwd)
BRANCH=$(git branch --show-current)
_pkgname=$NAME
pkgname=$_pkgname-git
pkgver=931651d
pkgrel=1
pkgdesc=
arch=("i686" "x86_64")
url="https://lxqt.org"
license=("GPL2")
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
source=("git+file:///home/stef/git/stefonarch/$NAME#branch=$BRANCH")
branch=$branch
sha256sums=('SKIP')


pkgver() {
  cd "$FOLDER"
  # use this for naming with branchname:
  #git branch --show-current
  # version naming:
  git describe --always | sed "s/-/./g"
}

build() {
  mkdir -p build
  cd build
  cmake "$srcdir/$_pkgname" \
    -DCMAKE_INSTALL_PREFIX=/usr
  make
}

branch() {
  cd "$srcdir/$_pkgname"
  git branch --show-current
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
