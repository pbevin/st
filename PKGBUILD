# Maintainer:

pkgname=st-pbevin-git
_pkgname=st
pkgver=0.8.4.r1178.7e6e779
pkgrel=5
epoch=1
pkgdesc="Pete's custom suckless terminal"
url=https://github.com/pbevin/st
arch=(i686 x86_64)
license=(MIT)
options=(zipman)
depends=(libx11 libxft dmenu xclip)
makedepends=(ncurses libxext git)
source=(git://github.com/LukeSmithxyz/st config.h)
sha1sums=(SKIP SKIP)

provides=("${_pkgname}")
conflicts=("${_pkgname}")

pkgver() {
	cd "${_pkgname}"
	printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
		"$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd $srcdir/${_pkgname}
	# skip terminfo which conflicts with ncurses
	sed -i '/tic /d' Makefile
        cp ../config.h config.h
}

build() {
	cd "${_pkgname}"
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd "${_pkgname}"
	make PREFIX=/usr DESTDIR="${pkgdir}" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
	install -Dm644 Xdefaults "${pkgdir}/usr/share/doc/${pkgname}/Xdefaults.example"
}
