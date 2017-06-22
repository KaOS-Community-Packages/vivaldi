pkgname=vivaldi
pkgver=1.10.867.42
pkgrel=1
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
source=("https://downloads.vivaldi.com/stable/${pkgname}-stable_${pkgver}-1_amd64.deb")
sha1sums=('e06d1ad6d0a6a6dc91088d6e05f4a80c43c90234')

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
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi/vivaldi-sandbox"
	msg "Installation finished!"
}
