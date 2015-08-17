#Maintainer: Yichao Yu <yyc1992@gmail.com>
#Contributor: Yichao Yu <yyc1992@gmail.com>

pkgname=python3-sympy-git
pkgver=20120222
pkgrel=2
pkgdesc="A Python library for symbolic mathematics. Python3 git version"
depends=('python' 'python-numpy')
arch=('i686' 'x86_64')
makedepends=('git')
install=
url="https://github.com/sympy/sympy"
license=('BSD')
provide=('python-sympy')
conflict=('python-sympy')

_gitroot=git://github.com/sympy/sympy.git
_gitname=sympy

build() {
  cd "${srcdir}"

  if [ -d ${_gitname} ]; then
    cd "${_gitname}"  || return 1
    git pull origin || return 1
    cd ..
  else
    git clone ${_gitroot} || return 1
  fi

  msg "GIT checkout done or server timeout"

  cd "${srcdir}/${_gitname}"

  bin/use2to3
  cd py3k-sympy/

  #somehow bin/isympy is not converted.
  2to3 -w bin/*

  python setup.py install --prefix=/usr --root "${pkgdir}" || return 1

  mv "${pkgdir}"/usr/bin/isympy "${pkgdir}"/usr/bin/isympy3
  mv "${pkgdir}"/usr/share/man/man1/isympy.1 "${pkgdir}"/usr/share/man/man1/isympy3.1
}
