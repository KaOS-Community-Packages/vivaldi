pkgname=vivaldi
pkgver=7.5.3735.74
pkgrel=1
pkgdesc='The web browser from Vivaldi / Vivaldi browser is made for power users in mind by people who love the Web.'
arch=('x86_64')
url='https://vivaldi.com'
license=('custom: Vivaldi')
depends=('gcc-libs' 'gtk3' 'nss' 'libjpeg-turbo' 'freetype2' 'cairo' 'libxslt'
         'libpng' 'alsa-lib' 'libxss' 'hicolor-icon-theme' 'xdg-utils'
         'widevine')
options=(!strip !emptydirs)
source=("https://downloads.vivaldi.com/stable/${pkgname}-stable-${pkgver}-1.x86_64.rpm")
sha256sums=('bf6ef0895aa04399ad4318ef4943fdf559b82fa02735370abd17862a96055185')

package() {
    msg 'Prepare dirs'
    install -dm755 "${pkgdir}/opt/${pkgname}"
    install -dm755 "${pkgdir}/usr/share"
    install -dm755 "${pkgdir}/usr/bin"

    msg 'Copy files'
    cp -r "${srcdir}/opt/${pkgname}/"* "${pkgdir}/opt/${pkgname}"
    install -Dm644 "${srcdir}/usr/share/appdata/${pkgname}.appdata.xml" \
        "${pkgdir}/usr/share/appdata/${pkgname}.appdata.xml"
    install -Dm644 "${srcdir}/usr/share/applications/${pkgname}-stable.desktop" \
        "${pkgdir}/usr/share/applications/${pkgname}-stable.desktop"

    msg 'Copy icons'
    local i
    for i in 16 22 24 32 48 64 128 256; do
        install -Dm644 "${pkgdir}/opt/${pkgname}/product_logo_${i}.png" \
            "${pkgdir}/usr/share/icons/hicolor/${i}x${i}/apps/${pkgname}.png"
    done

    msg 'Removing duplicated images'
    rm "${pkgdir}/opt/${pkgname}/product_logo_"*.png

    msg 'Linkings'
    ln -sf "/opt/${pkgname}/${pkgname}" "${pkgdir}/usr/bin/${pkgname}-stable"
    #rm "${pkgdir}/opt/${pkgname}/lib/libffmpeg.so"
    #ln -sf /usr/lib/chromium/libs/libffmpeg.so "${pkgdir}/opt/${pkgname}/libffmpeg.so.${pkgver%\.*\.*}"
    ln -sf /opt/google/chrome-unstable/WidevineCdm "${pkgdir}/opt/${pkgname}/WidevineCdm"

    msg 'Correct rights'
    chmod 4755 "${pkgdir}/opt/${pkgname}/vivaldi-sandbox"
    msg 'Installation finished!'
}
