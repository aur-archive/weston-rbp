# Maintainer: Srđan Tot

pkgname=weston-rbp
pkgver=1.4.0
pkgrel=1
pkgdesc='Reference implementation of a Wayland compositor for Raspberry Pi'
arch=('armv6h')
url='http://wayland.freedesktop.org'
license=('MIT')
depends=('libxkbcommon' 'poppler-glib' 'mtdev' 'libxcursor' 'pango' 'raspberrypi-firmware-tools')
conflicts=('weston')
provides=('weston')
source=("http://wayland.freedesktop.org/releases/weston-$pkgver.tar.xz"
	"bcm_host.pc"
	"egl.pc"
	"glesv2.pc"
	"$pkgname.install")
install=$pkgname.install
sha1sums=('49b0b6d5e2366a7bad5158b29998213e5ca7f254'
	  'f40a7a2e5ea69e4ec0327e3ba1d1fc31d70b01b0'
	  'dc64eb1bc41a85f32ddea5c006ae3181bd8222bb'
	  '01c011605b0590c4aa140cff1bf273cb03b1cfeb'
	  'e3494fa45fb9514f25946764326ebc674a0a5075')

build() {
	cd weston-$pkgver
	PKG_CONFIG_PATH="$srcdir" ./configure \
		--prefix=/usr \
		--libexecdir=/usr/lib/weston \
		--enable-demo-clients \
		--disable-x11-compositor --disable-drm-compositor \
		--disable-wayland-compositor \
		--enable-weston-launch --disable-simple-egl-clients --disable-egl \
		--disable-libunwind --disable-colord --disable-resize-optimization \
		--disable-xwayland-test --with-cairo=image \
		WESTON_NATIVE_BACKEND="rpi-backend.so"
	make
}

package() {
	cd weston-$pkgver
	make DESTDIR="$pkgdir" install
	# license
	install -Dm644 COPYING "$pkgdir/usr/share/licenses/weston/COPYING"
}
