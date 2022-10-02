# Maintainer: Daichi Shinozaki <dsdseg@gmail.com>
# Contributor: Vincent Bernardoff <vb@luminar.eu.org>#
# Contributor: lafka <lafa@hackeriet.no>
# Contributor: Albert Chang <albert.chang@gmx.com>
# Contributor: Thomas Mudrunka <harvie@@email..cz> You can also contact me on http://blog.harvie.cz/
# Contributor: zhehao

pkgname=riak
pkgver=3.0.10
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
backup=('etc/riak.conf')
install='riak.install'
source=(
    "git+https://github.com/basho/riak.git"
    #"https://github.com/basho/riak/archive/refs/tags/riak-3.0.10.tar.gz"
    'riak.service'
)
md5sums=('SKIP'
         '60c34e8ee8bc6d314df62b3b6d30ec96')

build() {
  cd "$srcdir/riak/"

  msg 'Building...'
  unset LDFLAGS
  make rel
}

package() {
  cd "$srcdir/riak/"
  
  install -d "$pkgdir/usr/lib"
  install -d "$pkgdir/var/log"
  install -d "$pkgdir/etc"
  install -d "$pkgdir/usr/share/doc"

  cp -a "rel/riak" "$pkgdir/usr/lib/riak"
  chmod -R 755 "$pkgdir/usr/lib/riak/bin"
  ln -s /usr/lib/riak/log "$pkgdir/var/log/riak"
  ln -s /usr/lib/riak/etc "$pkgdir/etc/riak"
  cp -R "doc/man" "$pkgdir/usr/share"
  cp -R "doc" "$pkgdir/usr/share/doc/riak"
  rm -R "$pkgdir/usr/share/doc/riak/man"
  chmod -R 755 "$pkgdir/usr/share"

  # install daemon
  install -Dm644 "$srcdir"/riak.service "$pkgdir"/usr/lib/systemd/system/riak.service
}
