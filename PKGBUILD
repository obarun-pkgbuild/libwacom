# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libwacom
# 						Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libwacom
pkgver=0.29
pkgrel=2
pkgdesc="Library to identify Wacom tablets and their features"
arch=('x86_64')
url="https://github.com/linuxwacom/libwacom/wiki"
license=('MIT')
depends=('glib2' 'libgudev')
makedepends=('libxml2')
source=(https://sourceforge.net/projects/linuxwacom/files/libwacom/$pkgname-$pkgver.tar.bz2)
sha256sums=('9cea00e68ddf342c3f749f6628d33fd3646f1937d7c57053ec6c5728d9a333b6')
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
