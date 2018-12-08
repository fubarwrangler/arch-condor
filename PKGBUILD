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
depends=('libcgroup' 'libvirt' 'python')
makedepends=('libvirt-devel')
checkdepends=()
optdepends=()
provides=('libclassad=8.8.0')
backup=(etc/condor/condor_config)
#options=()
install=htcondor.install
source=("$pkgname-$pkgver.tar.xz")
noextract=()
sha256sums=('6fad13339acc9af5eb036133eca1b736ebeecc14b0d001d4f13249face466a91')
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
	-DWANT_BOINC:BOOL=ON \
	-DWANT_GLEXEC:BOOL=OFF \
	-DWANT_MAN_PAGES:BOOL=ON \
	-DHAVE_BACKFILL:BOOL=OFF \
	-DHAVE_BOINC:BOOL=OFF \
	-DHAVE_KBDD:BOOL=OFF \
	-DWITH_BLAHP:BOOL=OFF \
	-DWITH_CREAM:BOOL=OFF \
	-DWITH_CAMPUSFACTORY:BOOL=OFF \
	-DWITH_COREDUMPER:BOOL=OFF \
	-DWITH_GLOBUS:BOOL=OFF \
	-DWITH_KRB5:BOOL=ON \
	-DWITH_MUNGE:BOOL=OFF \
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

	_docdir="$pkgdir/usr/share/doc/condor"
	_sharedir="$pkgdir/usr/share/condor"
	_confdir="$pkgdir/etc/condor"
	_pkglibdir="$pkgdir/usr/lib/condor"

	mkdir -p $_docdir $_sharedir

	# Move manpages
	mv "$pkgdir/usr/man $pkgdir/usr/share/"

	# Move /etc/ config to right place and put examples in docs
	mkdir -p $_confdir
	mkdir "$_confdir/config.d"
	mv "$pkgdir/usr/etc/condor/*" "$pkgdir/etc/condor/"
	mv "$pkgdir/usr/etc/examples/*" $_docdir
	rm -rf "$pkgdir/usr/etc/"
	rm -rf "$pkgdir/usr/examples/"
	
	# Last docs
	mv "$pkgdir/usr/LICENSE-2.0.txt" "$pkgdir/usr/README" $_docdir

	mkdir "$_pkglibdir"
	mv "$pkgdir/usr/libexec/*" $_pkglibdir
	rmdir "$pkgdir/usr/libexec"

}
