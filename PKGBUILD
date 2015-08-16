# Maintainer: Chris Brannon <chris@the-brannons.com>
# Contributor: Christoph Neuroth <christoph.neuroth@gmx.net>
# Contributor: Devin Christensen <quixoten at gmail dot com>
# Contributor: Mike Swanson <mikeonthecomputer@gmail.com>
pkgname=mmixware
pkgver=20131017
pkgrel=2
pkgdesc="A straightforward MMIX assembler and simulator"
arch=('i686' 'x86_64')
url=http://mmix.cs.hm.edu
# The license was taken from src/boilerplate.w.
license=('custom')
makedepends=('texlive-core')
source=(http://mmix.cs.hm.edu/src/mmix-$pkgver.tgz
        COPYRIGHT)
sha256sums=('aa64c4b9dc3cf51f07b330791f8ce542b0ae8a1132e098fa95a19b31350050b4'
            '3fb6e8d5258cb66aff24e22beb6eb338814395a2fe37b1cf70e21cfc54b9b4bf')
noextract=("mmix-$pkgver.tgz")

build() {
  mkdir "$srcdir/mmix-$pkgver"
  cd "$srcdir/mmix-$pkgver"
  tar -xzf "../mmix-$pkgver.tgz"

  unset MAKEFLAGS
  make {mmixal,mmix-{arith,config,doc,io,mem,pipe,sim},mmmix,mmotype}.pdf
  make all
}

package() {
  cd "$srcdir/mmix-$pkgver"

  install -m755 -d "$pkgdir/usr/src/$pkgname"
  tar --no-same-owner -C "$pkgdir/usr/src/$pkgname" -xf "../mmix-$pkgver.tgz"

  install -m755 -d "$pkgdir/usr/bin"
  install -m755 abstime mmix mmixal mmmix mmotype "$pkgdir/usr/bin"
  install -m755 -d "$pkgdir/usr/share/doc/$pkgname"
  install -m644 *.pdf "$pkgdir/usr/share/doc/$pkgname"
  install -D -m644 ../COPYRIGHT "$pkgdir/usr/share/licenses/$pkgname/COPYRIGHT"
}
