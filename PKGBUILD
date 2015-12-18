pkgname=vivaldi
<<<<<<< HEAD
pkgver=1.0.344.37
=======
pkgver=1.0.352.3
>>>>>>> bc52bd487f13afbd9a666a7815c11d8af2fb06fc
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils')
install=${pkgname}.install
<<<<<<< HEAD
_branch="beta"
source=("http://repo.vivaldi.com/archive/deb/pool/main/${pkgname}-${_branch}_${pkgver}-1_amd64.deb"
        "vivaldi-libffmpeg.zip")
#source=("https://vivaldi.com/download/${pkgname}-${_branch}_${pkgver}-1_amd64.deb")
md5sums=('571fed995097dfb9d13e1d6a535e2c14'
         'cd6836852f5f4a6a1fed13d5842b605e')
=======
_branch="snapshot"
source=("http://repo.vivaldi.com/archive/deb/pool/main/${pkgname}-${_branch}_${pkgver}-1_amd64.deb")
#source=("https://vivaldi.com/download/${pkgname}-${_branch}_${pkgver}-1_amd64.deb")
md5sums=('e09045a10b59682d555570bc114c598f')
>>>>>>> bc52bd487f13afbd9a666a7815c11d8af2fb06fc

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
<<<<<<< HEAD

	#Add ffmpeg (H.264/MP4) support 
	rm "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
	install -Dm644 "$srcdir"/libffmpeg.so "$pkgdir"/opt/vivaldi-${_branch}/lib/libffmpeg.so
=======
	
	
	
>>>>>>> bc52bd487f13afbd9a666a7815c11d8af2fb06fc
	msg "Authorizing Flash plugin (if present)"
	sed -i "s|chrome|chrome-unstable|g" "$pkgdir"/opt/vivaldi-${_branch}/vivaldi-${_branch}
	#Correct rights
	chmod 4755 "${pkgdir}/opt/vivaldi-${_branch}/vivaldi-sandbox"
	msg "Installation finished!"
}
