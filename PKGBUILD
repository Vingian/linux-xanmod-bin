_deb='https://github.com/xanmod/linux/releases/download/6.1.0-xanmod1/linux-image-6.1.0-x64v3-xanmod1_6.1.0-x64v3-xanmod1-0.20221213.629e4bb9_amd64.deb'
pkgname=linux-xanmod-edge-bin
pkgbase=linux-xanmod-edge-bin
_kernel=$(echo "$_deb" | sed 's/^.*linux-image-\([^_]*\).*$/\1/')
pkgver=$(echo "$_kernel" | sed 's/^\([0-9.]*\).*$/\1/')
pkgrel=$(echo "$_kernel" | sed 's/^.*xanmod\([0-9.]*\).*$/\1/')
pkgdesc='Linux Xanmod - Latest Mainline (EDGE)'
url='http://www.xanmod.org/'
arch=(x86_64)
license=(GPL2)
options=('!strip')
depends=(coreutils kmod initramfs)
optdepends=('crda: to set the correct wireless channels of your country' 'linux-firmware: firmware images needed for some devices')
provides=(VIRTUALBOX-GUEST-MODULES WIREGUARD-MODULE KSMBD-MODULE NTFS3-MODULE)
source=("$_deb")
sha512sums=('SKIP')

package() {
  pkgdesc='The Linux kernel and modules with Xanmod patches'

  tar -xf "$srcdir/data.tar.xz" -C "$pkgdir/"

  local modulesdir="usr/lib/modules/$_kernel"

  pushd "$pkgdir"
  rm -rf usr/*
  mv lib usr
  mv boot/vmlinuz-* "$modulesdir/vmlinuz"
  echo "${pkgbase%-*}" > "$modulesdir/pkgbase"
  find . -maxdepth 1 ! -name 'usr' -and ! -name '.' -exec rm -rf {} +
  popd
}
