# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=gnomeicu
pkgver=0.99.14
pkgrel=1
pkgdesc="A GNOME2 ICQ client."
arch=(i686 x86_64)
license=('GPL')
depends=('libgnomeui>=2.14.1' 'libxss')
makedepends=('pkgconfig' 'gnome-doc-utils' 'intltool')
url="http://gnomeicu.sourceforge.net/"
options=(!emptydirs)
install=gnomeicu.install
source=(http://downloads.sourceforge.net/sourceforge/${pkgname}/${pkgname}-${pkgver}.tar.bz2)
md5sums=('f5afc147590543f607a6b4efa0c69052')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sysconfdir=/etc \
              --localstatedir=/var || return 1
  make || return 1
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install || return 1

  install -m755 -d "${pkgdir}/usr/share/gconf/schemas"
  gconf-merge-schema ${pkgdir}/usr/share/gconf/schemas/${pkgname}.schemas --domain gnomeicu ${pkgdir}/etc/gconf/schemas/*.schemas
  rm -f ${pkgdir}/etc/gconf/schemas/*.schemas
}
