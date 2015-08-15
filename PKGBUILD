# Maintainer: SpepS <dreamspepser at yahoo dot it>

pkgname=dseq
pkgver=0.3.2b
pkgrel=2
pkgdesc="Desfonema Sequencer is a tracker-inspired MIDI sequencer."
arch=(i686 x86_64)
url="http://www.desfonema.com.ar/software.html"
license=('GPL')
depends=('pygtk' 'alsa-lib')
makedepends=('python2-distribute')
install="$pkgname.install"
source=("http://www.desfonema.com.ar/$pkgname/$pkgname-$pkgver.tar.bz2"
        "$pkgname.desktop")
md5sums=('39a7eadb63370fd53a60c977cf38d3a6'
         'eb84ee3fc967fbf2d84c5ffd49a0331f')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  # python2 fix
  sed -i "s|\(python\).*|\12|" $pkgname.py

  python2 setup.py build
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  # libs
  python2 setup.py install --root="$pkgdir/"

  # data
  install -d "$pkgdir/usr/share/$pkgname"
  install -Dm644 *.py $pkgname.png "$pkgdir/usr/share/$pkgname"
  cp -a midi "$pkgdir/usr/share/$pkgname"

  # bin
  install -d "$pkgdir/usr/bin"
  cat << EOF >> "$pkgdir/usr/bin/$pkgname"
cd /usr/share/$pkgname && python2 $pkgname.py \$@
EOF
  chmod +x "$pkgdir/usr/bin/$pkgname"

  # docs
  install -d "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 docs/* "$pkgdir/usr/share/doc/$pkgname"

  # desktop file
  install -Dm644 "$srcdir/$pkgname.desktop" \
    "$pkgdir/usr/share/applications/$pkgname.desktop"

  # icon
  install -Dm644 "${pkgname}48.png" \
    "$pkgdir/usr/share/pixmaps/$pkgname.png"
}

# vim:set ts=2 sw=2 et:
