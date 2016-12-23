pkgname=vivaldi
pkgver=1.6.689.46
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'chromium-ffmpeg-codecs')
optdepends=('pepper-flash: Pepper Flash plugin')
conflicts=('vivaldi-ffmpeg')
provides=('vivaldi-ffmpeg')
replaces=('vivaldi-ffmpeg')
backup=("opt/vivaldi/resources/vivaldi/style/custom.css")
source=("https://downloads.vivaldi.com/stable/${pkgname}-stable_${pkgver}-1_amd64.deb")
sha1sums=('7877a93bbe7767ff68c8388772c04c051098b867')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	for i in 16 22 24 32 48 64 128 256; do
        install -Dm644 "$pkgdir"/opt/vivaldi/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi.png
	done
	msg "Removing unsupported ffmpeg and duplicated images"
	rm "$pkgdir"/opt/vivaldi/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi/product_logo_*.png
	ln -s /usr/lib/chromium/libs/libffmpeg.so "$pkgdir"/opt/vivaldi/lib/libffmpeg.so
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi/vivaldi-sandbox"
	msg "Add a hack to modify UI"
	sed -i 's|^|@import "custom.css";|' "$pkgdir"/opt/vivaldi/resources/vivaldi/style/common.css
	touch "$pkgdir"/opt/vivaldi/resources/vivaldi/style/custom.css
	chmod 666 "$pkgdir"/opt/vivaldi/resources/vivaldi/style/custom.css
	msg "Installation finished!"
}
