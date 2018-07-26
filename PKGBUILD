pkgname=bcache-tools
_srcname=bcachefs-tools
pkgver=r364.b5094ee
pkgrel=1
pkgdesc="Tools for bcache filesystem"
arch=('x86_64')
url="https://bcachefs.org/"
depends=('util-linux' 'libscrypt' 'libsodium' 'liburcu' 'lz4' 'zlib' 'zstd')
makedepends=('linux-bcachefs-headers')
license=('GPL2')
source=("git+https://evilpiepirate.org/git/bcachefs-tools.git")
sha256sums=('SKIP')

pkgver() {
  cd "${_srcname}"

  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${_srcname}"

  # fix wrong include path
  sed 's|<attr/xattr\.h>|<sys/xattr.h>|' -i cmd_migrate.c
}

build() {
  cd "${_srcname}"

  make
}

package() {
  cd "${_srcname}"

  make DESTDIR="${pkgdir}" PREFIX="/usr" ROOT_SBINDIR="/usr/bin" install
  rm -r "${pkgdir}/usr/share/initramfs-tools"
}
