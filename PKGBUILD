# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
pkgname=condor
pkgver=8.8.0
pkgrel=1
pkgdesc="HTCondor High-Throughput Computing Batch System"
arch=("x86_64")
url="https://research.cs.wisc.edu/htcondor/"
license=('Apache')
groups=()
depends=('libcgroup')
makedepends=()
checkdepends=()
optdepends=()
# provides=('htcondor=8.8.0')
backup=(/etc/condor/condor_config)
#options=()
install=htcondor.install
source=("$pkgname-$pkgver.tar.xz")
noextract=()
md5sums=()
validpgpkeys=()

prepare() {
	cd "$pkgname-$pkgver"
}

build() {
	cd "$pkgname-$pkgver"
	cmake \
	-DUW_BUILD:BOOL=FALSE \
	-D_DEBUG:BOOL=TRUE \
	-D_VERBOSE:BOOL=FALSE \
	-DNO_PHONE_HOME:BOOL=TRUE \
	-DCLIPPED:BOOL=TRUE \
	-DCMAKE_BUILD_TYPE:STRING=Release \
	-DCMAKE_INSTALL_PREFIX:STRING=/usr \
	-DCMAKE_SKIP_RPATH:BOOL=ON \
	-DBUILD_SHARED_LIBS:BOOL=ON \
	-DWANT_FULL_DEPLOYMENT:BOOL=ON \
	-DWANT_GLEXEC:BOOL=OFF \
	-DWANT_MAN_PAGES:BOOL=ON \
	-DHAVE_BACKFILL:BOOL=OFF \
	-DHAVE_KBDD:BOOL=OFF \
	-DWITH_BLAHP:BOOL=OFF \
	-DWITH_BOINC:BOOL=OFF \
	-DWITH_CAMPUSFACTORY:BOOL=OFF \
	-DWITH_COREDUMPER:BOOL=OFF \
	-DWITH_GLOBUS:BOOL=OFF \
	-DWITH_KRB5:BOOL=ON \
	-DWITH_LIBCGROUP:BOOL=ON \
	-DWITH_LIBVIRT:BOOL=ON \
	-DWITH_LIBXML2:BOOL=ON \
	-DWITH_PYTHON_BINDINGS:BOOL=ON \
	-DWITH_OPENSSL:BOOL=ON \
	-DWITH_UNICOREGAHP:BOOL=OFF \
	-DWITH_VOMS:BOOL=OFF

	make
}

package() {
	cd "$pkgname-$pkgver"
	make DESTDIR="$pkgdir/" install
}
