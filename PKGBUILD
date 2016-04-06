pkgname=vivaldi
pkgver=1.0.435.40
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'vivaldi-ffmpeg')
optdepends=('pepper-flash: Pepper Flash plugin')
install=${pkgname}.install
source=("https://vivaldi.com/download/stable/${pkgname}-stable_${pkgver}-1_amd64.deb")
md5sums=('f721546fa040d7703eb458d40baea9c0')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
        install -Dm644 "$pkgdir"/opt/vivaldi/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi.png
	done
	msg "Removing unsupported ffmpeg and duplicated images"
	rm "$pkgdir"/opt/vivaldi/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi/product_logo_*.png
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi/vivaldi-sandbox"
	msg "Installation finished!"
}
