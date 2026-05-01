# Maintainer: josephgbr <rafael.f.f1@gmail.com>

# How to update?
# 'pkgver' and 'pkgrel' has to be same as in 'smbclient'
# Run 'pacman -Si smbclient' to verify the version
# e.g.: smbclient 4.1.8-1 means pkgver=4.1.8 and pkgrel=1

pkgbase=lib32-samba
pkgname=(lib32-libwbclient lib32-smbclient)
pkgver=4.20.1
pkgrel=1.0
arch=('x86_64')
url="http://www.samba.org"
license=('GPL3')
_urlprefix=https://mirror.archlinux32.org/i686/extra/
source=("$_urlprefix/smbclient-$pkgver-$pkgrel-i686.pkg.tar.zst"
        "$_urlprefix/libwbclient-$pkgver-$pkgrel-i686.pkg.tar.zst")
noextract=(smbclient-$pkgver-$pkgrel-i686.pkg.tar.zst
           libwbclient-$pkgver-$pkgrel-i686.pkg.tar.zst)
md5sums=('c460b3019130aeb5fc8545b8637f0ed1'
         '0cb6c4d89c6aca2749df831a143d4e14')

package_lib32-libwbclient() {
  pkgdesc="Samba winbind client library (32 bits)"
  depends=('lib32-libbsd' 'lib32-glibc' "libwbclient>=$pkgver")

  if pacman -Qi lib32-libbsd > /dev/null 2>&1; then
     rm -rf lib32-libbsd
     git clone --depth 1 https://aur.archlinux.org/lib32-libbsd.git
     cd lib32-libbsd
     makepkg -si
     cd ..
  fi

  rm -rf libwbclient && mkdir libwbclient
  cd libwbclient  
  tar xf ../libwbclient-$pkgver-$pkgrel-i686.pkg.tar.zst usr/lib
  
  mkdir -p "$pkgdir"/usr/lib32
  cp -rPf usr/lib/* "$pkgdir"/usr/lib32
  sed -i 's#/lib#/lib32#' "$pkgdir"/usr/lib32/pkgconfig/wbclient.pc
}


package_lib32-smbclient() {
  pkgdesc="Tools to access a server's filespace and printers via SMB (32 bits)"
  depends=('lib32-tdb' 'lib32-gnutls' 'lib32-talloc' 'lib32-libcap'
           'lib32-libwbclient' 'lib32-libgcrypt' 'lib32-libcups'
           'lib32-pam' 'lib32-avahi' 'lib32-systemd' 'lib32-acl'
           "smbclient>=$pkgver")
         
  rm -rf smbclient && mkdir smbclient
  cd smbclient  
  tar xf ../smbclient-$pkgver-$pkgrel-i686.pkg.tar.zst usr/lib
  
  mkdir -p "$pkgdir"/usr/lib32
  cp -rPf usr/lib/* "$pkgdir"/usr/lib32
  sed -i 's#/lib#/lib32#'\
    "$pkgdir"/usr/lib32/pkgconfig/netapi.pc \
    "$pkgdir"/usr/lib32/pkgconfig/smbclient.pc
    
  rm -rf "$pkgdir"/usr/lib32/cups # not a lib
}
