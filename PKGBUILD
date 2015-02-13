pkgname=vivaldi
pkgver=1.0.98.2
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('cusom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils')
install=${pkgname}.install
source=("http://vivaldi.com/download/snapshot/${pkgname}-snapshot_${pkgver}-1_amd64.deb")
md5sums=('33ae495b27582b771c2b183f55f4b38a')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi-snapshot/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
		install -Dm644 "$pkgdir"/opt/vivaldi-snapshot/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi.png
	done
  msg "Removing duplicated images"
  rm "$pkgdir"/opt/vivaldi-snapshot/product_logo_*.png
  msg "Installation finished!"
}
