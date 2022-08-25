# Maintainer: Leonid Pilyugin <l.pilyugin04@gmail.com>>

pkgname=kawaii-kscreenlocker
pkgver=5.25.4
pkgrel=1
pkgdesc='Library and components for kawaii secure lock screen architecture'
arch=(x86_64)
url='https://kde.org/plasma-desktop/'
license=(LGPL)
groups=(kawaii)
depends=(layer-shell-qt kidletime kwayland kdeclarative perl lightdm lightdm-webkit2-greeter)
makedepends=(extra-cmake-modules kdoctools kcmutils libxcursor)
optdepends=('kcmutils: configuration module')
provides=('kscreenlocker=5.25.4')
source=("https://download.kde.org/stable/plasma/$pkgver/kscreenlocker-$pkgver.tar.xz"
        "$pkgname-$pkgver.tar.gz::https://github.com/LeonidPilyugin/$pkgname/releases/download/v$pkgver/files.tar.gz")
sha256sums=('7dd3d20b38c156b676c5c84f2422491f28cbb7825de21ae37dbd77ec779bdb7d'
            '07c4df9406727ff5e7e13aa8d8345bf4a6a2930140878b0f18b9dfff5e5f4977')

build() {
    cmake -B build -S kscreenlocker-$pkgver \
        -DCMAKE_INSTALL_LIBEXECDIR=/usr/lib \
        -DBUILD_TESTING=OFF
    cmake --build build
}

package() {
    DESTDIR="$pkgdir" cmake --install build
    mv $pkgdir/usr/lib/kscreenlocker_greet $pkgdir/usr/lib/kscreenlocker_greet_exec
    install -m755 $srcdir/files/lock_script $pkgdir/usr/lib/kscreenlocker_greet
    mv $pkgdir/usr/lib64/* $pkgdir/usr/lib/
    rm -r $pkgdir/usr/lib64
}
