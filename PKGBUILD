# Maintainer Tyler Kaminski <durcor at disroot dot org>

pkgname=rocclr-git
_pkgname="${pkgname%-git}"
pkgver=aomp.3.5.0.r280.gaeb62482
pkgrel=1
pkgdesc='Radeon Open Compute Common Language Runtime'
arch=('x86_64')
url='https://github.com/ROCm-Developer-Tools/ROCclr'
license=('MIT')
depends=('mesa' 'comgr' 'hsa-rocr' 'hsakmt-roct' 'rocm-cmake')
makedepends=('cmake')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("${pkgname}::git+$url.git#branch=develop")
sha256sums=('SKIP')

pkgver() {
    cd "$pkgname"
    git describe --tags --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cmake -Wno-dev -B build \
        -S "$srcdir/$pkgname" \
		-DCMAKE_INSTALL_PREFIX='/opt/rocm/rocclr' \
		-DOPENCL_DIR="$srcdir/../../rocm-opencl-runtime/src/ROCm-OpenCL-Runtime-rocm-3.7.0"

    make -C build
}

package() {
    DESTDIR="$pkgdir" make -C build install
}
