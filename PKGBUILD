# Maintainer: Daniel Bermond <dbermond@archlinux.org>

_os="$( \
  uname \
    -o)"
_proj="rockchip"
_pkg="mpp"
pkgname="${_proj}-${_pkg}"
pkgver=1.0.7
pkgrel=1
epoch=1
pkgdesc='Rockchip Media Process Platform (MPP)'
arch=(
  'x86_64'
  'i686'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'pentium4'
  'powerpc'
)
_http="https://github.com"
_ns="${_proj}-linux"
url="${_http}/${_ns}/${_pkg}"
license=(
  'Apache-2.0'
  'MIT'
)
depends=(
)
if [[ "${_os}" == "GNU/Linux" ]]; then
  depends+=(
    'gcc-libs'
  )
elif [[ "${_os}" == "Android" ]]; then
  depends+=(
    'ndk-sysroot'
  )
fi
makedepends=(
  'cmake'
)
source=(
  "${url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha256sums=(
  '08fe9c1bdb72dbf93490cf6a633e6817b49667423e80a7b62be0aae97f883fd6'
)

build() {
  local \
    _cmake_opts=()
  _cmake_opts=(
    -DCMAKE_BUILD_TYPE:STRING='None'
    -DCMAKE_INSTALL_PREFIX:PATH='/usr'
    -DENABLE_VPROC_VDPP:BOOL='ON'
    -Wno-dev
  )
  cmake \
    -B \
      build \
    -S \
      "${_pkg}-${pkgver}" \
    -G 'Unix Makefiles' \
    "${_cmake_opts[@]}"
  cmake \
    --build \
      build
}

check() {
  ctest \
    --test-dir \
      build \
    --output-on-failure
}

package() {
  DESTDIR="${pkgdir}" \
  cmake \
    --install \
      build
  install \
    -Dm644 \
    "${_pkg}-${pkgver}/LICENSES/MIT" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE-MIT"
}
