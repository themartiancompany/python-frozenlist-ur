# Maintainer: Jelle van der Waa <jelle@vdwaa.nl>

_pyname=frozenlist
pkgname=python-${_pyname}
pkgver=1.4.1
pkgrel=2
pkgdesc='FrozenList is a list-like structure which can be made immutable'
url='https://github.com/aio-libs/frozenlist'
arch=('x86_64')
license=('Apache')
depends=('python')
makedepends=('cython' 'python-build' 'python-installer' 'python-wheel' 'python-setuptools' 'python-expandvars')
checkdepends=('python-pytest' 'python-pytest-cov')
source=(${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha512sums=('a82059fd7d16ec8e17cdf9d05eb128194fc3eed7c20ea4a3daf508a949e6c039fb5824794eac1ca768de11d883f55f46de45f5dcc5031f5cb31291b33df87023')
b2sums=('44ee864cd6c7918634d2db85937d778a8526f3117e4d27e06267c979bda2228de5bacaa87d8e0339f7718d6c12325336025214b8d42bdcc744aac7adb63b736a')

prepare() {
  cd "${_pyname}-${pkgver}"
  sed 's|.install-cython ||' -i Makefile
}

build() {
  cd "${_pyname}-${pkgver}"
  make cythonize
  python -m build --wheel --no-isolation
}

check() {
  cd "${_pyname}-${pkgver}"
  python -m venv --system-site-packages test-env
  test-env/bin/python -m installer dist/*.whl
  test-env/bin/python -m pytest
}

package() {
  cd "${_pyname}-${pkgver}"
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
  install -Dm 644 CHANGES.rst README.rst -t "${pkgdir}/usr/share/doc/${pkgname}"
}

# vim: ts=2 sw=2 et:
