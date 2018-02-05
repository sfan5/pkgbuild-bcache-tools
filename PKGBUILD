pkgname=bcache-tools
_srcname=bcachefs-tools
pkgver=r304.99adc23
pkgrel=1
pkgdesc="Tools for bcache filesystem"
arch=('x86_64')
url="https://bcachefs.org/"
depends=('util-linux' 'libscrypt' 'libsodium' 'liburcu')
makedepends=('linux-bcachefs-headers')
license=('GPL2')
source=("git+https://evilpiepirate.org/git/bcachefs-tools.git")
sha256sums=('SKIP')

pkgver() {
  cd "${_srcname}"

  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${_srcname}"

  make
}

package() {
  cd "${_srcname}"

  make DESTDIR="${pkgdir}" ROOT_SBINDIR="/usr/bin" install
}
