# Maintainer: Alexandre Demers <alexandre.f.demers@gmail.com>

_pkgbasename=dav1d
pkgname=lib32-$_pkgbasename
pkgver=0.5.1
pkgrel=1
pkgdesc='AV1 cross-platform decoder focused on speed and correctness (32 bit)'
url='https://code.videolan.org/videolan/dav1d/'
arch=('x86_64')
license=('BSD')
depends=(
      "$_pkgbasename"
      'lib32-glibc'
      'lib32-vulkan-icd-loader'
      )
makedepends=(
      'meson'
      'ninja'
      'nasm'
      'doxygen'
      'vulkan-headers'
      )
source=(https://downloads.videolan.org/pub/videolan/${_pkgbasename}/${pkgver}/${_pkgbasename}-${pkgver}.tar.xz{,.asc}
        'lib32.meson')
sha256sums=('ad69f9eb4cc8c722048307b1ea13f72d9c1be2a7f45c7c12ceb7101793338e0d'
            'SKIP'
            '0852227a4b8e2367d73727645203da45ead1834773458e2fc109d30e40e12221')
validpgpkeys=('65F7C6B4206BD057A7EB73787180713BE58D1ADC') # VideoLAN Release Signing Key

prepare() {
  cd ${_pkgbasename}-${pkgver}

  # Patching if needed
}

build() {
  cd ${_pkgbasename}-${pkgver}
  arch-meson build \
    --cross-file=../lib32.meson \
    --libdir=/usr/lib32

  ninja -C build
}

check() {
  cd ${_pkgbasename}-${pkgver}/build
  meson test
}

package() {
  cd ${_pkgbasename}-${pkgver}

  DESTDIR="${pkgdir}" ninja -C build install
  rm -rf "$pkgdir"/usr/{include,share,bin}
}
