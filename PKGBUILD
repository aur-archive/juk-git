pkgname=juk-git
pkgver=20121001
pkgrel=1
pkgdesc="JuK is an audio jukebox application"
arch=('i686' 'x86_64')
url="http://www.kde.org/applications/multimedia/juk/"
license=('GPL')
depends=('kdelibs' 'kdebase-runtime' 'taglib-extras' 'xdg-utils')
makedepends=('git' 'cmake' 'automoc4')
conflicts=('kdemultimedia-juk')
provides=('kdemultimedia-juk')
replaces=('kdemultimedia-juk')
install='juk-git.install'
md5sums=()

_gitroot="git://anongit.kde.org/juk.git"
_gitname="juk"

build() {
  cd $startdir/src

  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"

  cd $srcdir/$_gitname-build
  cmake . -DCMAKE_INSTALL_PREFIX=$( kde4-config --prefix ) || return 1
  make || return 1
  make DESTDIR="$pkgdir" install
}
