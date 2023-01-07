# Maintainer: Daichi Shinozaki <dsdseg@gmail.com>
# Contributor: Vincent Bernardoff <vb@luminar.eu.org>#
# Contributor: lafka <lafa@hackeriet.no>
# Contributor: Albert Chang <albert.chang@gmx.com>
# Contributor: Thomas Mudrunka <harvie@@email..cz> You can also contact me on http://blog.harvie.cz/
# Contributor: zhehao

pkgname=riak
pkgver=3.2.0
pkgrel=1
pkgdesc='NOSQL database engine providing decentralized key-value store, flexible map/reduce engine and HTTP/JSON query interface'
arch=('i686' 'x86_64')
license=('APACHE')
url=http://docs.basho.com/riak/latest/downloads/
conflicts=('tsung')
#makedepends=('erlang-nox-r17' 'java-environment')
makedepends=()
optdepends=()
options=('!makeflags')
backup=('etc/riak/riak.conf')
install='riak.install'
source=(
    "git+https://github.com/basho/riak.git#branch=develop"
    #"https://github.com/basho/riak/archive/refs/tags/riak-3.0.10.tar.gz"
    'riak.service'
)
md5sums=('SKIP'
         'SKIP')

build() {
  cd "$srcdir/riak/"

  msg 'Building...'
  unset LDFLAGS
  make rel
}

package() {
  cd "$srcdir/riak/"
  
  install -d "$pkgdir/usr/lib/riak/"
  install -d "$pkgdir/var/log"
  install -d "$pkgdir/etc"
  install -d "$pkgdir/usr/share/doc"

  sed -i 's|platform_bin_dir = ./bin|platform_bin_dir = /usr/lib/riak/bin/|' rel/riak/etc/riak.conf
  sed -i 's|platform_etc_dir = ./etc|platform_etc_dir = /etc/riak/|' rel/riak/etc/riak.conf
  sed -i 's|platform_lib_dir = ./lib|platform_lib_dir = /usr/lib/riak/lib/|' rel/riak/etc/riak.conf
  sed -i 's|platform_data_dir = ./data|platform_data_dir = /var/lib/riak/|' rel/riak/etc/riak.conf
  sed -i 's|platform_log_dir = ./log|platform_log_dir = /var/log/riak/|' rel/riak/etc/riak.conf
  install -D "rel/riak/etc/riak.conf" "$pkgdir/etc/riak/riak.conf"
  install -D "rel/riak/etc/advanced.config" "$pkgdir/etc/riak/advanced.config"
  mkdir "$pkgdir/usr/bin/"
  install "rel/riak/usr/bin/riak" "$pkgdir/usr/bin/"


  cp -R "rel/riak/" "$pkgdir/usr/lib/"
  cp -R "doc/man" "$pkgdir/usr/share"
  cp -R "rel/riak/share/schema" "$pkgdir/usr/share/"

  cp -R "doc" "$pkgdir/usr/share/doc/riak"
  rm -R "$pkgdir/usr/share/doc/riak/man"
  chmod -R 755 "$pkgdir/usr/share"

  # install daemon
  install -Dm644 "$srcdir"/riak.service "$pkgdir"/usr/lib/systemd/system/riak.service
  install -Dm644 "$srcdir"/riak.service "$pkgdir"/usr/lib/systemd/system/riak.service
}
