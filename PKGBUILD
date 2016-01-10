pkgname=vivaldi
pkgver=1.0.365.3
pkgbase=48.0.2564.48
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
source=("http://repo.vivaldi.com/archive/deb/pool/main/${pkgname}-${_branch}_${pkgver}-1_amd64.deb"
        "ffmpeg-v${pkgbase}.tar.gz::https://github.com/Gabrielgtx/ffmpeg/archive/v${pkgbase}.tar.gz")
md5sums=('acb7ae0f1405e57e2ac81c81d0a607a0'
         'c835f635fd8d72493b00f6f021a78505')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi-${_branch}/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
		install -Dm644 "$pkgdir"/opt/vivaldi-${_branch}/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi-${_branch}.png
	done
	msg "Removing duplicated images"
	rm "$pkgdir"/opt/vivaldi-${_branch}/product_logo_*.png
	#add ffmpeg (H.264/MP4) support
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	install -Dm644 "$srcdir"/ffmpeg-${pkgbase}/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	msg "Authorizing Flash plugin (if present)"
	sed -i "s|chrome|chrome-unstable|g" "$pkgdir"/opt/vivaldi-${_branch}/vivaldi-${_branch}
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
