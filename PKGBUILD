# Maintainer: Mariano Verdu <verdumariano@gmail.com>
pkgname=plecost-svn
pkgver=2
pkgrel=2
pkgdesc="Wordpress finger printer tool search and retrieve information about the plugins versions installed in Wordpress systems."
arch=('i686' 'x86_64')
url="http://code.google.com/p/plecost/"
license=('GPL3')
depends=('python2')
makedepends=('subversion')
provides=('plecost')
md5sums=() 

_svntrunk=http://plecost.googlecode.com/svn/trunk/
_svnmod=plecost

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD
  #
  
  mkdir -p "$pkgdir/usr/share/"
  cp -r "$srcdir/$_svnmod" "$pkgdir/usr/share/"
  sed -i "s#!/usr/bin/python#!/usr/bin/python2#g" "$pkgdir/usr/share/plecost/plecost-0.2.2-8-beta.py"
  
  mkdir -p "$pkgdir/usr/bin/"
  touch "$pkgdir/usr/bin/plecost"
  echo "/usr/share/plecost/plecost-0.2.2-8-beta.py" > "$pkgdir/usr/bin/plecost"
  chmod 777 "$pkgdir/usr/bin/plecost"
}
