# Maintainer: Your Name <youremail@domain.com>
pkgname=test-dotnet-makepkg-arch-git
pkgrel=1
arch=(x86_64)
url=""
license=('GPL')
groups=()
depends=("dotnet-runtime>=9.0")
makedepends=("git" "dotnet-sdk>=9.0")
provides=("${pkgname}")
conflicts=("${pkgname}")
replaces=()
backup=()
options=()
install=
source=('git+https://github.com/melon095/test-dotnet-makepkg-arch')
noextract=()
sha256sums=('SKIP')

_carch="x64"
_framework='net9.0'
_runtime="linux-${_carch}"
_outdir="${pkgver}/${_framework}/${_runtime}"
_branch='develop'

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "$srcdir/${pkgname%-git}"

    dotnet restore \
        --runtime "${_runtime}" \
        --locked-mode
}

build() {
	cd "$srcdir/${pkgname%-git}"

    dotnet build \
        --framework "${_framework}" \
        --runtime "${_runtime}" \
        --configuration Release \
        --output "${_outdir}"
}

package() {
	cd "$srcdir/${pkgname%-git}"

    cp -dr "${_outdir}/*" "${pkgdir}/usr/lib/test-dotnet-makepkg-arch/bin"

    install -Dm644 etc/test-dotnet-makepkg-arch.service "${pkgdir}/usr/lib/systemd/test-dotnet-makepkg-arch.service"
    install -Dm644 etc/test-dotnet-makepkg-arch.sysusers "${pkgdir}/usr/lib/sysusers.d/test-dotnet-makepkg-arch.conf"
    install -Dm644 etc/test-dotnet-makepkg-arch.tmpfiles "${pkgdir}/usr/lib/tmpfiles.d/test-dotnet-makepkg-arch.conf"
}

