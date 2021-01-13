pkgname=dwm-pie
_pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
conflicts=(dwm)
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
	dwm-pie-menu
	dwm-pie-scrot
	dwm.desktop
	https://dwm.suckless.org/patches/vanitygaps/dwm-vanitygaps-6.2.diff)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            'SKIP'
            'SKIP'
            'SKIP'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            '2bb07d33e2dafcb737014db99840556dbbeee716db6d5dfeacee3b0027cd4cc1')

prepare() {
  cd "$srcdir/$_pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
  patch --forward --strip=1 --input="${srcdir}/dwm-vanitygaps-6.2.diff"
}

build() {
  cd "$srcdir/$_pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$_pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
  install -m755 -D "$srcdir/dwm-pie-menu" "$pkgdir/usr/bin/dwm-pie-menu"
  install -m755 -D "$srcdir/dwm-pie-scrot" "$pkgdir/usr/bin/dwm-pie-scrot"
}
