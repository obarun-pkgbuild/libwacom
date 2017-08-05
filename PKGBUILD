# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libwacom
# 						Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom
pkgver=0.24
pkgrel=1
pkgdesc="Library to identify Wacom tablets and their features"
arch=('x86_64' 'i686')
url="https://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Libwacom"
license=('MIT')
depends=('glib2' 'libgudev')
source=(https://sourceforge.net/projects/linuxwacom/files/libwacom/${pkgname}-$pkgver.tar.bz2)
sha256sums=('2905a0ee5cc85eceb9f5bd06109e66a051b0ed18102c3e6798717c259c8d66c3')
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