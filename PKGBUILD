pkgname=garlicurl
_pkgname=curl
provides=('curl')
conflicts=('curl')
pkgver=8.11.0
pkgrel=4
pkgdesc="An URL retrival utility and library"
arch=('x86_64' 'aarch64')
url="https://curl.se/"
license=('MIT')
depends=('zlib' 'openssl' 'bash' 'ca-certificates' 'libssh2' 'libpsl' 'libidn2' 'libnghttp2')
options=('!libtool')
source=("https://curl.se/download/${_pkgname}-${pkgver}.tar.bz2"
        'garlicurl.diff'
        "https://github.com/curl/curl/commit/49ced6160bec578259f0d4f72a93bdfa4f4c0a83.diff")
md5sums=('5ba1f5d144166ea9a5a828c57f7728b0'
         'f70fbd9907996c1555aa5ad4a8f2a8eb'
         'fbd6e3ceb5f92b83e86433c254f70e4c')

build() {
    cd ${_pkgname}-${pkgver}
    patch -p1 -i ${srcdir}/garlicurl.diff

    ./configure \
        --with-random=/dev/urandom \
        --prefix=/usr \
        --mandir=/usr/share/man \
        --enable-ipv6 \
        --disable-ldaps \
        --disable-ldap \
        --enable-manual \
        --enable-versioned-symbols \
        --enable-threaded-resolver \
        --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt \
        --with-libssh2 \
        --with-openssl \
        --with-fish-functions-dir=/usr/share/fish/vendor_completions.d/completions
    make
}

package() {
    cd ${_pkgname}-${pkgver}
    make DESTDIR=${pkgdir} install

    install -Dm644 COPYING ${pkgdir}/usr/share/licenses/${_pkgname}/COPYING
    install -Dm644 docs/libcurl/libcurl.m4 ${pkgdir}/usr/share/aclocal/libcurl.m4
}
