pkgname=vivaldi
pkgver=2.9.1705.31
_pkgver=${pkgver}-1
pkgrel=2
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk3' 'nss' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils' 'chromium-ffmpeg-codecs' 'widevine')
optdepends=('pepper-flash: Pepper Flash plugin')
conflicts=('vivaldi-ffmpeg')
provides=('vivaldi-ffmpeg')
replaces=('vivaldi-ffmpeg')
source=("https://downloads.vivaldi.com/stable/${pkgname}-stable_${_pkgver}_amd64.deb")
md5sums=('b6900b68446882fda2799aa7636ebecf')

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
	#ln -sf /opt/google/chrome-unstable/WidevineCdm/_platform_specific/linux_x64/libwidevinecdm.so "$pkgdir"/opt/vivaldi/libwidevinecdm.so
	ln -sf /opt/google/chrome-unstable/WidevineCdm "${pkgdir}/opt/vivaldi/WidevineCdm"
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi/vivaldi-sandbox"
	msg "Installation finished!"
}
