# Maintainer: Kyle Keen <keenerd@gmail.com>
# Contributor: Marq Schneider <queueRAM@gmail.com>

# Modifications: Yawning Angel <yawning@schwanenlied.me>
#
# Use the github mirror instead of a version control system no one else uses.


pkgname=kicad-git
pkgver=78d9e7b
pkgrel=1
pkgdesc="Electronic schematic and printed circuit board (PCB) design tools"
arch=('i686' 'x86_64')
url="http://iut-tice.ujf-grenoble.fr/kicad/"
license=('GPL')
depends=('glew' 'wxgtk' 'hicolor-icon-theme' 'desktop-file-utils' 'boost-libs')
makedepends=('cmake' 'zlib' 'mesa' 'boost')
optdepends=('kicad-docs-bzr: for documentation'
            'kicad-library-git: for footprints'
            'kicad-pretty-git: for more footprints'
            'git: github pcb plugin')
conflicts=('kicad' 'kicad-bzr')
provides=('kicad')
install=kicad.install
source=('git+https://github.com/KiCad/kicad-source-mirror.git')
md5sums=('SKIP')

# mkdir -p "$pkgdir/etc/profile.d"
# echo "export KIGITHUB=https://github.com/KiCad" > "$pkgdir/etc/profile.d/kicad.sh"
# https://github.com/blairbonnett-mirrors/kicad/blob/master/scripts/kicad-install.sh

pkgver() {
  cd "$srcdir/kicad-source-mirror"
  git rev-parse --short HEAD
}

build() {
  cd "$srcdir/kicad-source-mirror"
  mkdir -p build/Release
  cd build/Release
  # -DKICAD_SKIP_BOOST=ON ?
  # -DKICAD_SCRIPTING=ON -DKICAD_SCRIPTING_MODULES=ON ?
  # -DKICAD_SCRIPTING_WXPYTHON=ON ?
  cmake ../.. -DCMAKE_BUILD_TYPE=Release \
              -DCMAKE_INSTALL_PREFIX=/usr \
              -DKICAD_SKIP_BOOST=ON \
              -DBUILD_GITHUB_PLUGIN=ON
  make #-j1
}

package() {
  cd "$srcdir/kicad-source-mirror/build/Release"
  make DESTDIR="$pkgdir" install
}
