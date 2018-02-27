# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libwacom
# 						Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom
pkgver=0.28
pkgrel=3
pkgdesc="Library to identify Wacom tablets and their features"
arch=('x86_64')
url="http://linuxwacom.sourceforge.net/wiki/index.php/Libwacom"
license=('MIT')
depends=('glib2' 'libgudev')
source=(https://sourceforge.net/projects/linuxwacom/files/libwacom/$pkgname-$pkgver.tar.bz2
        fix-pairedid-entry.patch)
sha256sums=('e7d632301288b221cb5af69b4c5e57fd062bafd9a9acd6f9ce271570103267ef'
            'ed9a5500359c84d7f8784025185c7e66df7726d52b74170e15c17d64d871d51b')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  cd $pkgname-$pkgver
  patch -Np1 -i ../fix-pairedid-entry.patch
}

build() {
  cd ${pkgname}-$pkgver
  ./configure --prefix=/usr
  make
}

check() {
  cd ${pkgname}-$pkgver
  make check
}

package() {
  cd ${pkgname}-$pkgver
  make DESTDIR="$pkgdir" install
  install -D -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -m755 -d ${pkgdir}/usr/lib/udev/rules.d
  cd tools
  ./generate-udev-rules > ${pkgdir}/usr/lib/udev/rules.d/65-libwacom.rules
  
}
