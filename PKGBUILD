# Maintainer: Ner0

pkgname=trine2
_gamepkg=trine2_linux_installer.run
pkgver=1.16
pkgrel=1
pkgdesc="A sidescrolling game of action, puzzles and platforming where you play as one of Three Heroes"
arch=('i686' 'x86_64')
url="http://trine2.com/"
license=('custom: commercial')
makedepends=('bash')
source=("$pkgname.sh")
md5sums=('d4deb264ed647b54d8e3a9351c879527')

if [ "$CARCH" == 'i686' ]; then
   depends=('mesa' 'freetype2' 'openal' 'libogg' 'libvorbis' 'gcc-libs' 'glibc' 'bzip2' 'gtk2' 'libgl'
            'atk' 'glib2' 'pango' 'gdk-pixbuf2' 'fontconfig' 'libxxf86vm' 'libsm' 'libx11' 'libpng')
elif [ "$CARCH" == 'x86_64' ]; then
   depends=('lib32-mesa' 'lib32-freetype2' 'lib32-openal' 'lib32-libogg' 'lib32-libvorbis' 'lib32-gcc-libs'
            'lib32-glibc' 'lib32-bzip2' 'lib32-gtk2' 'lib32-atk' 'lib32-glib2' 'lib32-pango' 'lib32-gdk-pixbuf2'
            'lib32-fontconfig' 'lib32-libxxf86vm' 'lib32-libsm' 'lib32-libx11' 'lib32-libpng' 'lib32-libgl')
fi

# Uncomment this to reduce the compression time
# PKGEXT='.pkg.tar'

package () {
   msg "You need a full copy of this game in order to install it"
   msg "Searching for ${_gamepkg} in dir: \"$startdir\""
	 pkgpath=$startdir
   if [[ ! -f "$startdir/${_gamepkg}" ]]; then
       error "Game package not found, please type absolute path to ${_gamepkg} (/home/joe):"
       read pkgpath
       if [[ ! -f "${pkgpath}/${_gamepkg}" ]]; then
           error "Unable to find game package." && return 1
       fi
    fi
    msg "Found game package, installing..."

  msg "Extracting the game (this may take a while)..."
  # "--install-to=" doesn't work, must temporary override $HOME
  HOME="$pkgdir/usr/share" sh "$pkgpath/$_gamepkg" --non-interactive &>/dev/null

  mv "$pkgdir/usr/share/Trine2" "$pkgdir/usr/share/trine2"
  cd "$pkgdir/usr/share/trine2"

  install -Dm644 trine2.png "$pkgdir/usr/share/pixmaps/trine2.png"
  install -Dm644 trine2.desktop "$pkgdir/usr/share/applications/trine2.desktop"
  install -Dm755 "$srcdir/$pkgname.sh" "$pkgdir/usr/bin/trine2"

  sed -e 's/Exec=.*/Exec=\/usr\/bin\/trine2/' \
      -e 's/Icon=.*/Icon=\/usr\/share\/pixmaps\/trine2.png/' \
      -i "$pkgdir/usr/share/applications/trine2.desktop"

  rm -f README* KNOWN* trine2.*
}
