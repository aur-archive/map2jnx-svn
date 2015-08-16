# Maintainer: Alexander Drozdov <adrozdoff@gmail.com>
pkgname=map2jnx-svn
pkgver=3373
pkgrel=4
pkgdesc="GeoTIFF to JNX (Garmin BirdsEye) format converter"
arch=('i686' 'x86_64')
url="https://qlandkartegt.svn.sourceforge.net/svnroot/qlandkartegt/map2jnx/trunk/"
license=('GPL')
groups=('qlandkartegt')
depends=(gdal proj libjpeg)
makedepends=('subversion')
provides=('map2jnx')
conflicts=('map2jnx')
replaces=('map2jnx')
source=('proj-480.patch' 'force-jnx-scale-support.diff')

_svntrunk=https://qlandkartegt.svn.sourceforge.net/svnroot/qlandkartegt/map2jnx/trunk
_svnmod=map2jnx

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"
  
  # my patch already present in upstream
  #patch -p0 < "${srcdir}"/proj-480.patch
  #patch -p0 < "${srcdir}"/force-jnx-scale-support.diff

  #
  # BUILD
  #
  cmake -DCMAKE_INSTALL_PREFIX=/usr .
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}

md5sums=('b5b83fe595fbe3b37793c61717639a2f'
         'e65e4aecfe72509d88d76747f6abc8b6')
