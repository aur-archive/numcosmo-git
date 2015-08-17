# Maintainer: Sandro Dias Pinto Vitenti <sandro@isoftware.com.br>

pkgname=numcosmo-git
_gitname=numcosmo
pkgver=v0.12.1
pkgrel=1
pkgdesc="Numerical Cosmology - NumCosmo"
url="https://savannah.nongnu.org/projects/numcosmo/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('glib2' 'gsl' 'gmp' 'mpfr' 'sundials' 'sqlite3' 'fftw' 'nlopt' 'cfitsio' 'gtk-doc' 'glib2-docs')
optdepends=('atlas-lapack')
provides=('numcosmo')
conflicts=('numcosmo')
source=('git+http://git.savannah.gnu.org/r/numcosmo.git')
#source=('git+file:///home/sandro/Projects/numcosmo')
md5sums=('SKIP')
#options=(debug !strip)

pkgver() {
  cd $_gitname
  echo $(git describe --always --abbrev=0).$(git rev-list --count HEAD)
}

build() {
  NCPU=`grep processor /proc/cpuinfo | wc -l`

  cd $_gitname

  rm -rf "$srcdir/$_gitname-build"
  mkdir "$srcdir/$_gitname-build"

  msg "Running autogen.sh ..."
  NOCONFIGURE=yes ./autogen.sh

  msg "Configuring ..."
  cd "$srcdir/$_gitname-build"
  "$srcdir/$_gitname"/configure --prefix=/usr --enable-shared --with-thread-pool-max=$NCPU --enable-gtk-doc --enable-man --enable-introspection
}

package() {
  cd $srcdir/$_gitname-build
  make DESTDIR=$pkgdir install
}
