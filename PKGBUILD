pkgname=bcache-tools
_srcname=bcache-tools
pkgver=0.9.r133.g7e714d2
pkgrel=1
pkgdesc="Tools for bcache filesystem"
arch=('i686' 'x86_64')
url="http://bcache.evilpiepirate.org/Bcachefs/"
depends=('util-linux' 'libnih' 'libscrypt' 'libsodium' 'liburcu')
makedepends=('linux-bcachefs-headers')
license=('GPL2')
source=("git+http://evilpiepirate.org/git/bcache-tools.git#branch=dev")
sha256sums=('SKIP')

pkgver() {
  cd "${_srcname}"

  git describe --tags --long | sed -E 's/^v//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd "${_srcname}"

  # fix broken include
  rm include/trace/events/bcache.h
  ln -s {/usr/lib/modules/4.8.0-bcachefs/build/,}include/trace/events/bcache.h
  make
}

package() {
  cd "${_srcname}"

  mkdir -p "${pkgdir}/usr/bin"
  mkdir -p "${pkgdir}/usr/share/man/man8"
  make DESTDIR="${pkgdir}" ROOT_SBINDIR="/usr/bin" install
}
