pkgname=vivaldi
pkgver=1.0.283.8
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url="https://vivaldi.com"
license=('custom: Vivaldi')
options=('!strip' '!emptydirs')
depends=('gcc-libs' 'gtk2' 'nss' 'gconf' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils')
install=${pkgname}.install
source=("http://repo.vivaldi.com/archive/deb/pool/main/${pkgname}-snapshot_${pkgver}-1_amd64.deb")
#source=("https://vivaldi.com/download/snapshot/${pkgname}-snapshot_${pkgver}-1_amd64.deb")
md5sums=('f8d4841becab9560cbca3d5b74d6d616')

package() {
	msg "Extracting Vivaldi"
	bsdtar -xf data.tar.xz -C "${pkgdir}/" 
	msg2 "Done extracting!"
	msg "Actual installation"
	ln -s /usr/lib/libudev.so.1 "${pkgdir}/opt/vivaldi-snapshot/libudev.so.0"
	for i in 16 22 24 32 48 64 128 256; do
		install -Dm644 "$pkgdir"/opt/vivaldi-snapshot/product_logo_${i}.png "$pkgdir"/usr/share/icons/hicolor/${i}x${i}/apps/vivaldi.png
	done
	msg "Removing duplicated images"
	rm "$pkgdir"/opt/vivaldi-snapshot/product_logo_*.png
	msg "Authorizing Flash plugin (if present)"
	sed -i "s|chrome|chrome-unstable|g" "$pkgdir"/opt/vivaldi-snapshot/vivaldi-snapshot
	msg "Installation finished!"
}
