# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libwacom
# 						Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom
pkgver=0.27
pkgrel=2
pkgdesc="Library to identify Wacom tablets and their features"
arch=('x86_64')
url="http://linuxwacom.sourceforge.net/wiki/index.php/Libwacom"
license=('MIT')
depends=('glib2' 'libgudev')
source=(https://sourceforge.net/projects/linuxwacom/files/libwacom/${pkgname}-$pkgver.tar.bz2)
sha256sums=('f340d0010cc5dece8e4523b1e3220a98cba7939450ddbc017e86a134ceaece14')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

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
