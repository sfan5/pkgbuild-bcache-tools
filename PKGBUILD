pkgname=bcache-tools
_srcname=bcachefs-tools
pkgver=r1081.c8bec83
pkgrel=1
pkgdesc="Tools for bcache filesystem"
arch=('x86_64')
url="https://bcachefs.org/"
depends=('util-linux' 'libaio' 'libsodium' 'liburcu' 'lz4' 'zlib' 'zstd')
makedepends=('cargo' 'linux-bcachefs-headers' 'clang' 'valgrind')
license=('GPL2')
source=("git+https://evilpiepirate.org/git/bcachefs-tools.git"
        "bcachefs-install"
        "bcachefs-hooks")
sha256sums=('SKIP'
            '45e38cc030bc87b707589ccb2d9d80018292e3b00c4472ce497e409ffbaaf31b'
            '7e5e8c657b62e6a398d966c4fc1c837062c2595cf28ad49fe9eae61b29c27688')

pkgver() {
  cd "${_srcname}"

  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${_srcname}/rust-src"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${_srcname}"

  export RUSTUP_TOOLCHAIN=stable
  make CARGO_ARGS="--frozen"
}

package() {
  cd "${_srcname}"

  make DESTDIR="${pkgdir}" PREFIX="/usr" ROOT_SBINDIR="/usr/bin" install
  rm -r "${pkgdir}/usr/share/initramfs-tools"

  # add mkinitcpio hook
  install -D -m644 "${srcdir}/bcachefs-install" "${pkgdir}/etc/initcpio/install/bcachefs"
  install -D -m644 "${srcdir}/bcachefs-hooks" "${pkgdir}/etc/initcpio/hooks/bcachefs"
}
