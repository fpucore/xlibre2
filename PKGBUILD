# Maintainers: Chris McGimpsey-Jones <chrisjones.unixmen@gmail.com>, artist <artist@artixlinux.org>, callmetango
# Contributors: AndyRTR <andyrtr@archlinux.org>, Jan de Groot <jgc@archlinux.org>

pkgbase=xlibre2-xserver
_pkgbase="${pkgbase%-*}"
pkgname=(xlibre2-xserver xlibre2-xephyr xlibre2-xvfb xlibre2-xnest xlibre2-common xlibre2-devel)
pkgver=26.8.0
pkgrel=2
arch=('x86_64')
license=('LicenseRef-Adobe-Display-PostScript'
         'BSD-3-Clause' 
         'LicenseRef-DEC-3-Clause' 
         'HPND'
         'LicenseRef-HPND-sell-MIT-disclaimer-xserver'
         'HPND-sell-variant' 
         'ICU'
         'ISC'
         'MIT'
         'MIT-open-group'
         'NTP'
         'SGI-B-2.0'
         'SMLNJ'
         'X11'
         'X11-distribute-modifications-variant')
groups=('xlibre')
url="https://www.freedompublishersunion.net/h-linux.html"
makedepends=('xorgproto' 'pixman' 'libx11'
             'libxkbfile' 'libxfont2' 'libpciaccess' 'libxv' 'libxcvt'
             'libxmu' 'libxrender' 'libxi' 'libxaw' 'libxtst' 'libxres'
             'xorg-xkbcomp' 'xorg-util-macros' 'xorg-font-util' 'libepoxy'
             'xcb-util' 'xcb-util-image' 'xcb-util-renderutil' 'xcb-util-wm' 'xcb-util-keysyms'
             'libxshmfence' 'libunwind' 'systemd' 'meson')

# derived src  "https://github.com/X11Libre/xserver/archive/refs/tags/xlibre-xserver-25.2.0.tar.gz"
# master src   "https://github.com/X11Libre/xserver/archive/refs/heads/master.zip"
source=(xvfb-run
        xvfb-run.1)

prepare() {
  cd "src/xlibre2-xserver-${pkgver}"
}

build() {
  export CFLAGS=${CFLAGS/-fno-plt}
  export CXXFLAGS=${CXXFLAGS/-fno-plt}
  export LDFLAGS=${LDFLAGS/-Wl,-z,now}

  arch-meson xlibre2-xserver-${pkgver} build \
    --buildtype=release \
    -D ipv6=true \
    -D xvfb=true \
    -D xnest=true \
    -D xcsecurity=true \
    -D xorg=true \
    -D xephyr=true \
    -D xfbdev=true \
    -D glamor=true \
    -D udev=true \
    -D udev_kms=true \
    -D dtrace=false \
    -D seatd_libseat=false \
    -D systemd_logind=true \
    -D suid_wrapper=true \
    -D linux_acpi=false \
    -D xkb_dir=/usr/share/X11/xkb \
    -D xkb_output_dir=/var/lib/xkb \
    -D libunwind=true

  # Print config
  meson configure build
  ninja -C build

  # fake installation to be seperated into packages
  DESTDIR="${srcdir}/fakeinstall" ninja -C build install

  # clean up this for irrelevance
  rm -f \
    "${srcdir}/fakeinstall/usr/share/man/man1/Xkdrive.1"
}

_install() {
  local src f dir
  for src; do
    f="${src#fakeinstall/}"
    dir="${pkgdir}/${f%/*}"
    install -m755 -d "${dir}"
    # use copy so a new file is created and fakeroot can track properties such as setuid
    cp -av "${src}" "${dir}/"
    rm -rf "${src}"
  done
}

package_xlibre2-common() {
  pkgdesc="A fork of the XLibre build of the X server common files."
  depends=('xkeyboard-config' 'xorg-xkbcomp' 'xorg-setxkbmap')
  provides=('xlibre-xserver-common' 'xlibre-xserver-common=25.1' 'xorg-server-common')
  conflicts=('xlibre-xserver-common' 'xorg-server-common' "xorg-server<$pkgver")

  _install fakeinstall/usr/lib/xorg/protocol.txt
  _install fakeinstall/usr/share/man/man1/Xserver.1

  # license
  install -m644 -Dt "${pkgdir}/usr/share/licenses/${pkgname}" ${_pkgbase}-xserver-${pkgver}/COPYING
}

package_xlibre2-xserver() {
  pkgdesc="A fork of the XLibre build of the X server."
  depends=('xlibre2-input-libinput' 'xlibre2-common' 'libepoxy' 'libxfont2' 'pixman' 'libunwind' 
          'dbus' 'libgl' 'nettle' 'libxdmcp' 'sh' 'glibc' 'libxau' 'libtirpc' 'libbsd' 'systemd-libs')
  provides=('xorg-server' 'xlibre-xserver=25.1' 'X-ABI-VIDEODRV_VERSION=28.0' 'X-ABI-XINPUT_VERSION=26.0' 'X-ABI-EXTENSION_VERSION=11.0' 'x-server' 'x11win-server')
  conflicts=('xlibre-xserver' 'xorg-server' 'nvidia-utils<=331.20' 'glamor-egl' 'xf86-video-modesetting')
  replaces=('xlibre-xserver' 'glamor-egl' 'xf86-video-modesetting')

  _install fakeinstall/usr/bin/{X,Xorg,gtf,Xfbdev}
  _install fakeinstall/usr/lib/Xorg{,.wrap}
  _install fakeinstall/usr/lib/xorg/modules/*
  _install fakeinstall/usr/share/X11/xorg.conf.d/10-{nvidia,nvidia-modules,quirks}.conf
  _install fakeinstall/usr/share/man/man1/{Xorg,Xorg.wrap,gtf,Xfbdev}.1
  _install fakeinstall/usr/share/man/man4/{exa,fbdevhw,inputtestdrv,modesetting}.4
  _install fakeinstall/usr/share/man/man5/{Xwrapper.config,xorg.conf,xorg.conf.d}.5

  # distro specific files must be installed in /usr/share/X11/xorg.conf.d
  install -m755 -d "${pkgdir}/etc/X11/xorg.conf.d"

  # license
  install -m644 -Dt "${pkgdir}/usr/share/licenses/${pkgname}" ${_pkgbase}-xserver-${pkgver}/COPYING
}

package_xlibre2-xephyr() {
  pkgdesc="A fork of the XLibre build of the nested X server that runs as an X application."
  depends=('xlibre2-common' 'libxfont2' 'libgl' 'libepoxy' 'libunwind' 'systemd-libs' 'pixman' 
          'xcb-util-image' 'xcb-util-renderutil' 'xcb-util-wm' 'xcb-util-keysyms' 'nettle' 
          'libtirpc' 'xcb-util' 'libxdmcp' 'libx11' 'libxau' 'libxshmfence' 'glibc')
  provides=('xlibre-xserver-xephyr' 'xorg-server-xephyr')
  conflicts=('xlibre-xserver-xephyr' 'xorg-server-xephyr')

  _install fakeinstall/usr/bin/Xephyr
  _install fakeinstall/usr/share/man/man1/Xephyr.1

  # license
  install -m644 -Dt "${pkgdir}/usr/share/licenses/${pkgname}" ${_pkgbase}-xserver-${pkgver}/COPYING
}

package_xlibre2-xvfb() {
  pkgdesc="A fork of the XLibre build of the X.Org virtual framebuffer X server."
  # xvfb-run is GPLv2, rest is MIT
  license=('MIT' 'GPL-2.0-only')
  depends=('xlibre2-common' 'libxfont2' 'libunwind' 'pixman' 'xorg-xauth' 'libgl' 'nettle' 'libtirpc' 'systemd-libs')
  provides=('xlibre-xserver-xvfb' 'xorg-server-xvfb')
  conflicts=('xlibre-xserver-xvfb' 'xorg-server-xvfb')

  _install fakeinstall/usr/bin/Xvfb
  _install fakeinstall/usr/share/man/man1/Xvfb.1

  install -m755 "${srcdir}/xvfb-run" "${pkgdir}/usr/bin/"
  install -m644 "${srcdir}/xvfb-run.1" "${pkgdir}/usr/share/man/man1/"

  # license
  install -m644 -Dt "${pkgdir}/usr/share/licenses/${pkgname}" ${_pkgbase}-xserver-${pkgver}/COPYING
}

package_xlibre2-xnest() {
  pkgdesc="A fork of the XLibre build of the X.Org nested X server that runs as an X application."
  depends=('xlibre2-common' 'libxfont2' 'libunwind' 'pixman' 'xorg-xauth' 'libgl' 'nettle' 'libtirpc' 'systemd-libs')
  provides=('xlibre-xserver-xnest' 'xorg-server-xnest')
  conflicts=('xlibre-xserver-xnest' 'xorg-server-xnest')

  _install fakeinstall/usr/bin/Xnest
  _install fakeinstall/usr/share/man/man1/Xnest.1

  # license
  install -m644 -Dt "${pkgdir}/usr/share/licenses/${pkgname}" ${_pkgbase}-xserver-${pkgver}/COPYING
}

package_xlibre2-devel() {
  pkgdesc="A fork of the XLibre build of the X.Org development files."
  depends=('xlibre2-xserver' 'xorgproto' 'libpciaccess' 'pixman' 'xorg-util-macros')
  provides=('xlibre-xserver-devel' 'xorg-server-devel')
  conflicts=('xlibre-xserver-devel' 'xorg-server-devel' 'xlibre-xserver-beta-debug')

  _install fakeinstall/usr/include/xorg/*
  _install fakeinstall/usr/lib/pkgconfig/xorg-server.pc
  _install fakeinstall/usr/lib/pkgconfig/xlibre-server.pc
  _install fakeinstall/usr/share/aclocal/xorg-server.m4

  rm fakeinstall/etc/X11/xorg.conf.d/10-nvidia-modules.conf.debian
  rm fakeinstall/etc/X11/xorg.conf.d/10-nvidia.conf.debian
#  rm fakeinstall/usr/share/X11/xorg.conf.d/10-nvidia-modules.conf

  # license
  install -m644 -Dt "${pkgdir}/usr/share/licenses/${pkgname}" ${_pkgbase}-xserver-${pkgver}/COPYING

  # make sure there are no files left to install
  find fakeinstall -depth -print0 | xargs -0 rmdir
}
sha256sums=('SKIP'
            'SKIP')
