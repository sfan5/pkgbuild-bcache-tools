pkgname=bcache-tools
_srcname=bcache-tools
pkgver=0.9.r126.g580ec04
pkgrel=1
pkgdesc="Tools for bcache filesystem"
arch=('i686' 'x86_64')
url="http://bcache.evilpiepirate.org/Bcachefs/"
depends=('util-linux' 'libnih' 'libscrypt' 'libsodium')
license=('GPL2')
source=("git+http://evilpiepirate.org/git/bcache-tools.git#branch=dev")
sha256sums=('SKIP')

pkgver() {
  cd "${_srcname}"

  git describe --tags --long | sed -E 's/^v//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd "${_srcname}"

  sed -i 's/-static//' Makefile
  make
}

package() {
  cd "${_srcname}"

  mkdir -p "${pkgdir}/usr/bin"
  mkdir -p "${pkgdir}/usr/share/man/man8"
  make DESTDIR="${pkgdir}" ROOT_SBINDIR="/usr/bin" install
}
