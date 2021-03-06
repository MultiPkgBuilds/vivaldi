pkgname=vivaldi
pkgver=1.7.735.46
pkgrel=2
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'chromium-ffmpeg-codecs' 'widevine')
optdepends=('pepper-flash: Pepper Flash plugin')
conflicts=('vivaldi-ffmpeg')
provides=('vivaldi-ffmpeg')
replaces=('vivaldi-ffmpeg')
backup=("opt/vivaldi/resources/vivaldi/style/custom.css")
source=("https://downloads.vivaldi.com/stable/${pkgname}-stable_${pkgver}-1_amd64.deb"
	"vivaldi-stable.desktop")
sha1sums=('9f8e3c44bf0ef0789ddafb9bfa47d34dd4ebb5ac'
	  '02e70dd8a915530e8b802d069766523bde56b3f2')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	local i
	for i in 16 22 24 32 48 64 128 256; do
        install -Dm644 "$pkgdir"/opt/vivaldi/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi.png
	done
	msg "Removing unsupported ffmpeg and duplicated images"
	rm "$pkgdir"/opt/vivaldi/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi/product_logo_*.png
	ln -s /usr/lib/chromium/libs/libffmpeg.so "$pkgdir"/opt/vivaldi/lib/libffmpeg.so
	ln -sf /opt/google/chrome-unstable/libwidevinecdm.so "$pkgdir"/opt/vivaldi/libwidevinecdm.so
	mv -f vivaldi-stable.desktop "$pkgdir"/usr/share/applications/vivaldi-stable.desktop
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi/vivaldi-sandbox"
	msg "Add a hack to modify UI"
	sed -i 's|^|@import "custom.css";|' "$pkgdir"/opt/vivaldi/resources/vivaldi/style/common.css
	touch "$pkgdir"/opt/vivaldi/resources/vivaldi/style/custom.css
	chmod 666 "$pkgdir"/opt/vivaldi/resources/vivaldi/style/custom.css
	msg "Installation finished!"
}
