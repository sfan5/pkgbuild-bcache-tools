pkgname=bcache-tools
_srcname=bcache-tools
pkgver=0.9.112.gf45d84c
pkgrel=1
pkgdesc="Tools for bcache filesystem"
arch=('i686' 'x86_64')
url="http://bcache.evilpiepirate.org/#index1h1"
depends=('util-linux' 'libnih')
license=('GPL2')
source=("git+http://evilpiepirate.org/git/bcache-tools.git#branch=dev")
sha256sums=('SKIP')

pkgver() {
  cd "${_srcname}"

  git describe --tags --long | sed -E 's/^v//;s/-/./g'
}

build() {
  cd "${_srcname}"

  sed -i 's/-Werror//;s/-static//;s|/sbin/|/bin/|;s|^UDEVLIBDIR=.*|UDEVLIBDIR=/usr/lib/udev|' Makefile
  make
}

package() {
  cd "${_srcname}"

  mkdir -p "${pkgdir}/usr/bin"
  mkdir -p "${pkgdir}/usr/lib/udev/rules.d"
  mkdir -p "${pkgdir}/usr/share/man/man8"
  make DESTDIR="${pkgdir}" install
}
