pkgname=vivaldi
pkgver=1.0.357.5
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils')
install=${pkgname}.install
_branch="snapshot"
source=("http://repo.vivaldi.com/archive/deb/pool/main/${pkgname}-${_branch}_${pkgver}-1_amd64.deb"
        "https://github.com/Gabrielgtx/ffmpeg/archive/master.zip")
md5sums=('757e424f1c8481fd78d2ceb9654a9eb9' 'SKIP')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi-${_branch}/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
		install -Dm644 "$pkgdir"/opt/vivaldi-${_branch}/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi.png
	done
	msg "Removing duplicated images"
	rm "$pkgdir"/opt/vivaldi-${_branch}/product_logo_*.png
	#add ffmpeg (H.264/MP4) support
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	install -Dm644 "$srcdir"/ffmpeg-master/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	msg "Authorizing Flash plugin (if present)"
	sed -i "s|chrome|chrome-unstable|g" "$pkgdir"/opt/vivaldi-${_branch}/vivaldi-${_branch}
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
