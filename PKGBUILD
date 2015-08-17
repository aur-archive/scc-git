# Maintainer: Michał Maciej Różański <michal.rozanski@gmail.com>
pkgname=scc-git
pkgver=20120718
pkgrel=3
pkgdesc="Simple Chat Client is a lightweight and simple program which allows talking in the chat onet.pl without using a browser or java."
arch=('i686' 'x86_64')
url="http://simplechatclien.sourceforge.net/"
license=('GPL')
depends=('qt' 'qca' 'qca-ossl' 'phonon')
conflicts=('scc')
makedepends=('git')

_gitroot="git://github.com/simplechatclient/simplechatclient.git"
_gitname="simplechatclient"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
  
  cmake . && make
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
}
