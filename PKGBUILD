#Mantainer: Anthony25
pkgname=subsonic-kang-git
pkgver=20140924
pkgrel=1
pkgdesc="Open-source web-based media streamer and jukebox fork of Subsonic with a no license patch, by KHresearch (git version)."
url="https://github.com/KHresearch/subsonic"
arch=('i686' 'x86_64' 'armv6h')
license=('GPL')
conflicts=('subsonic' 'subsonic-beta' 'subsonic-kang')
depends=('java-runtime-headless' 'libcups')
makedepends=('maven' 'git')
source=($pkgname-$pkgver::'git+https://github.com/KHresearch/subsonic.git'
	'subsonic.service')
backup=('var/subsonic/db'
    'var/subsonic/subsonic.sh')

build() {
  cd $srcdir/"$pkgname-$pkgver"
  git checkout release
  mvn -P full -Dmaven.test.skip=true -pl subsonic-main -am install
  mvn -P full -Dmaven.test.skip=true -pl subsonic-booter -am install
}

package() {
  cd $srcdir/"$pkgname-$pkgver"
  mkdir -p $pkgdir/var/subsonic
  mkdir -p $pkgdir/usr/lib/systemd/system
  cp subsonic-booter/src/main/script/subsonic.sh $pkgdir/var/subsonic/
  chmod +x $pkgdir/var/subsonic/subsonic.sh
  cp subsonic-booter/target/subsonic-booter-jar-with-dependencies.jar $pkgdir/var/subsonic/
  cp subsonic-main/{Getting\ Started.html,README.TXT,LICENSE.TXT} $pkgdir/var/subsonic
  cp subsonic-main/target/subsonic.war $pkgdir/var/subsonic
  cp $srcdir/subsonic.service $pkgdir/usr/lib/systemd/system
}

md5sums=('SKIP'
         '6525b6c6cb9693f99585b6fcd28995cd')
