# Maintainer: Leonid Pilyugin <l.pilyugin04@gmail.com>>

pkgname=kawaii-kscreenlocker
pkgver=5.26.1
pkgrel=1
pkgdesc='Library and components for kawaii secure lock screen architecture'
groups=(kawaii)
url='https://github.com/LeonidPilyugin/kawaii-kscreenlocker'
arch=(x86_64)
license=('LGPL')
depends=(layer-shell-qt kidletime kwayland kdeclarative perl lightdm lightdm-webkit2-greeter)
makedepends=(extra-cmake-modules kdoctools kcmutils libxcursor)
optdepends=('kcmutils: configuration module')
provides=('kscreenlocker=5.26.0')
conflicts=('kscreenlocker')
source=("https://download.kde.org/stable/plasma/$pkgver/kscreenlocker-$pkgver.tar.xz"
        "$pkgname-$pkgver.tar.gz::https://github.com/LeonidPilyugin/$pkgname/releases/download/v$pkgver/files.tar.gz")
sha256sums=('de315b9cdf0309b1e1ea0b57a79aa30b42493742604f17ae003e7d8f4f76867d'
            '05fbcd013d9bfd5568b633df7fbd67c3e75bfa4740785e45141679e0d585a604')

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
