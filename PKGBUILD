# Maintainer:  Charles Briere <charlesbriere.flatzo@gmail.com>

pkgname=bump-git
pkgver=20121208
pkgrel=1
pkgdesc="Bump is a library designed to make asynchronous programming easy by providing high-level data structures for concurrency management, including multi-threading and main loop callbacks, in GObject/GIO based projects, especially those written in Vala."
arch=('i686' 'x86_64')
url="https://code.google.com/p/bump/"
depends=('glibc' 'vala' 'libgee-0.8')
makedepends=('git')
license=('GPL')

_gitroot="https://code.google.com/p/bump"
_gitname="bump"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    ( cd $_gitname && git pull origin )
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  rm -rf "${_gitname}_build"
  cp -r "${_gitname}"{,_build}
  cd "${_gitname}_build"
  
  ./autogen.sh --prefix=/usr
  
  make
}

package()
{
    cd "${srcdir}/${_gitname}_build"
    make DESTDIR=$pkgdir install
}
