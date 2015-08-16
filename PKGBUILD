# Maintainer: Nathan Typanski <n.typanski at gmail dot com>

pkgname=libdrm-prime-git
pkgrel=1
pkgver=2.4.15.439.g364e52a
pkgdesc="Dave Airlie's prime branch of interface to kernel DRM services"
url="http://dri.freedesktop.org/"
arch=('i686' 'x86_64')
license=('MIT')
depends=('libpciaccess')
provides=('libdrm=$pkgver')
conflicts=('libdrm')
makedepends=('git' 'cairo' 'udev' 'valgrind')
options=('!libtool')
changelog=CHANGELOG
source=('libdrm-prime-git::git://people.freedesktop.org/~airlied/drm.git#branch=prime')
md5sums=('SKIP')

# pkgver() {
#     cd 'drm'
#     git describe --always | sed 's|libdrm.||g;s|-|.|g'
# }

pkgver() {
    cd $pkgname
    git describe --always | sed 's|libdrm.||g;s|-|.|g'
}

build() {
    cd $pkgname
    sed -i 's/PKG_CHECK_MODULES(PTHREADSTUBS, pthread-stubs)//' configure.ac

    ./autogen.sh
    ./configure --prefix=/usr \
		--enable-udev \
		--enable-intel \
		--enable-radeon \
		--enable-nouveau \
		--enable-vmwgfx
    make V=1
}

check() {
    cd $pkgname
    make -k check
}

package() {
    cd $pkgname
    make DESTDIR="$pkgdir" install
}
