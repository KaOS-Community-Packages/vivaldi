pkgname=vivaldi
pkgver=1.0.340.7
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
        "http://cqoicebordel.free.fr/vivffmpeg/lin64/libffmpeg.so.zip")
#source=("https://vivaldi.com/download/${pkgname}-${_branch}_${pkgver}-1_amd64.deb"
#        "http://cqoicebordel.free.fr/vivffmpeg/lin64/libffmpeg.so.zip")
md5sums=('5eb55821769e17d8c88763ddf4a8a158'
         '9d4e871958b0ecb41cadc600ce220f57')

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
	#Add ffmpeg support
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	install -Dm644 "$srcdir"/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	msg "Authorizing Flash plugin (if present)"
	sed -i "s|chrome|chrome-unstable|g" "$pkgdir"/opt/vivaldi-${_branch}/vivaldi-${_branch}
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
