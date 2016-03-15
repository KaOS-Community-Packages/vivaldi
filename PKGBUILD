pkgname=vivaldi
pkgver=1.0.422.8
pkgbase=49.0.2623.91
pkgrel=1
_branch="snapshot"
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils')
install=${pkgname}.install
source=("https://vivaldi.com/download/${_branch}/${pkgname}-${_branch}_${pkgver}-1_amd64.deb"
        "ffmpeg-v${pkgbase}.tar.gz::https://github.com/Gabrielgtx/ffmpeg/archive/v${pkgbase}.tar.gz")
md5sums=('d38ab5a9637cc4a32846107e6009008f'
         'd51df4dd3aefd8db72aba7a97fa445ea')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi-${_branch}/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
		install -Dm644 "$pkgdir"/opt/vivaldi-${_branch}/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi-${_branch}.png
	done
	msg "Removing unsupported ffmpeg and duplicated images"
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	rm "$pkgdir"/opt/vivaldi-${_branch}/product_logo_*.png
	msg "installing ffmpeg official support (H.264)"
	install -Dm644 "$srcdir"/ffmpeg-${pkgbase}/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	msg "Authorizing Flash plugin (if present)"
	sed -i "s|chrome|chrome-unstable|g" "$pkgdir"/opt/vivaldi-${_branch}/vivaldi-${_branch}
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
