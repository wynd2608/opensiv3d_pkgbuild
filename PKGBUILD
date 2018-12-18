_opencvrev=ab981c2c628168d5dd4acb979672305d7c9bdc07

pkgname=opensiv3d
pkgdesc="OpenSiv3D a C++ 17 framework for games and interactive media"
pkgver=r2626.ab981c2c
pkgrel=1
arch=('x86_64')
url="https://github.com/Siv3D/OpenSiv3D/"
license=('MIT')
depends=('boost' 'glew' 'glib2' 'libpng' 'libjpeg-turbo' 'libx11' 'libxi' 'libxrandr' 'libxinerama' 'libxcursor' 'freetype2' 'harfbuzz' 'openal' 'opencv' 'box2d' 'systemd' 'upower')
makedepends=('cmake' 'clang' 'pkg-config')
OPTIONS=(!strip docs !libtool staticlibs emptydirs zipman purge upx debug)

source=(opensiv3d::git+https://github.com/Siv3D/OpenSiv3D.git#commit=${_opencvrev})

sha1sums=('SKIP')

pkgver() {
	cd "$pkgname"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "${srcdir}/opensiv3d/Linux"
	git checkout linux

	[[ -d build ]] || mkdir build
	cd build

	sed -i -e 's/opencv/opencv4/' ${srcdir}/opensiv3d/Linux/CMakeLists.txt

	cmake \
	  -DCMAKE_BUILD_TYPE=Release \
	  -DCMAKE_INSTALL_PREFIX=/usr \
	  ${srcdir}/opensiv3d/Linux
	make

}

package() {
	install -Dm644 ${srcdir}/opensiv3d/LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	
	cd "${srcdir}/opensiv3d/Linux/build"
	make DESTDIR="${pkgdir}/" install

	sed -i -e 's/opencv4/opencv/' ${srcdir}/opensiv3d/Linux/CMakeLists.txt
}
