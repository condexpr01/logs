# Maintainer: condexpr01(Vito Devlin) <condexpr01@outlook.com>
PACKAGER='condexpr01(Vito Devlin) <condexpr01@outlook.com>'
pkgname=logs
pkgver=2026.02.03.1
pkgrel=1
pkgdesc='all kind of logs'
arch=('any')
url='https://github.com/condexpr01/logs'

license=('unlicense')

#depends=()
#makedepends=('pandoc' 'gzip')

source=('readme.md' 'LICENSE.txt' 'logs')
sha256sums=('SKIP' 'SKIP' 'SKIP')

prefix=${PREFIX:-/usr}

prepare() {
	cp -r "$startdir"/animation_log "$srcdir/"
	cp -r "$startdir"/earth_online_log "$srcdir/"
	cp -r "$startdir"/game_log "$srcdir/"
}

package() {
	if command -v pandoc 2>/dev/null >/dev/null; then
		pandoc -s -t man "$srcdir/readme.md" -o "$srcdir/readme.1"
		gzip -9c "$srcdir/readme.1" > "$srcdir/${pkgname}.gz"
		install -Dm644 "$srcdir/${pkgname}.gz" "$pkgdir${prefix}/share/man/man1/${pkgname}.1.gz"
	else
		echo "Warning: no pandoc, won't install man doc"
	fi

	install -Dm644 "$srcdir/LICENSE.txt" "$pkgdir${prefix}/share/license/${pkgname}/LICENSE.txt"
	
	install -Dm755 "$srcdir/logs" "$pkgdir${prefix}/bin/logs"

	install -dm755 "$pkgdir${prefix}/share/logs"

	cp -r "$srcdir"/animation_log "$pkgdir${prefix}/share/logs"
	cp -r "$srcdir"/earth_online_log "$pkgdir${prefix}/share/logs"
	cp -r "$srcdir"/game_log "$pkgdir${prefix}/share/logs"

	find "$pkgdir${prefix}/share/logs" -type f -exec chmod 666 {} \;
}
