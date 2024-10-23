# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Jelle van der Waa <jelle@vdwaa.nl>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pkg=frozenlist
pkgname="${_py}-${_pkg}"
pkgver=1.4.1
pkgrel=2
pkgdesc='FrozenList is a list-like structure which can be made immutable'
_http="https://github.com"
_ns="aio-libs"
url="${_http}/${_ns}/${_pkg}"
arch=(
  'x86_64'
  'i686'
  'armv7l'
  'arm'
  'aarch64'
  'mips'
  'pentium4'
  'powerpc'
)
license=(
  'Apache'
)
depends=(
  "${_py}>=${_pymajver}"
)
makedepends=(
  'cython'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
  "${_py}-setuptools"
  "${_py}-expandvars"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-cov"
)
source=(
  "${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  'a82059fd7d16ec8e17cdf9d05eb128194fc3eed7c20ea4a3daf508a949e6c039fb5824794eac1ca768de11d883f55f46de45f5dcc5031f5cb31291b33df87023'
)
b2sums=(
  '44ee864cd6c7918634d2db85937d778a8526f3117e4d27e06267c979bda2228de5bacaa87d8e0339f7718d6c12325336025214b8d42bdcc744aac7adb63b736a'
)

prepare() {
  cd \
    "${_pkg}-${pkgver}"
  sed \
    's|.install-cython ||' \
    -i \
    Makefile
}

build() {
  cd \
    "${_pkg}-${pkgver}"
  make \
    cythonize
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      venv \
    --system-site-packages \
    test-env
  test-env/bin/"${_py}" \
    -m \
      installer \
    dist/*.whl
  test-env/bin/"${_py}" \
    -m \
      pytest
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="$pkgdir" \
    dist/*.whl
  install \
    -Dm 644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -Dm 644 \
    CHANGES.rst \
    README.rst \
    -t \
    "${pkgdir}/usr/share/doc/${pkgname}"
}

# vim: ts=2 sw=2 et:
