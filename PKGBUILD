## SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# $Id: PKGBUILD 266875 2017-11-15 14:29:11Z foutrelis $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Henrique C. Alves <hcarvalhoalves@gmail.com>

_os="$( \
  uname \
    -o)"
_gconf="false"
_expat="true"
if [[ "${_expat}" == "true" ]]; then
  if [[ "${_os}" == "Android" ]]; then
    _libexpat="libexpat"
  elif [[ "${_os}" == "GNU/Linux" ]]; then
    _libexpat="expat"
  fi
fi
_proj="yoctoproject"
_pkg=matchbox
pkgname="${_pkg}-window-manager"
pkgver=1.2.2
_commit="844f61069896fe3f549ab425d731c061028f697c"
pkgrel=1
_pkgdesc=(
  "A pretty much unique X window manager"
  "with a classic PDA management policy"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'i686'
  'arm'
  'armv7l'
  'aarch64'
  'mips'
  'pentium4'
)
license=(
  'GPL'
)
depends=(
  'libmatchbox'
  'startup-notification'
  'libpng'
  'libsm'
  'libxcursor'
)
if [[ "${_expat}" == "true" ]]; then
  depends=(
    "${_libexpat}"
  )
  makedepends=(
    "${_libexpat}"
  )
fi
if [[ "${_gconf}" == "true" ]]; then
  depends=(
    'gconf'
  )
fi
makedepends=(
  'gconf'
)
url="http://${_pkg}-project.org/"
_http="https://git.${_proj}.org"
_ns="${pkgname}"
_url="${_http}/${_ns}"
_tarname="${pkgname}-${_commit}"
source=(
  "${_url}/snapshot/${pkgname}-${_commit}.tar.gz"
)
sha256sums=(
  '2f3f48ee2281f3ad6deab6f6b34c09af7978a384d8b8599193aa1edb6965c7ac'
)

build() {
  local \
    _cflags=() \
    _configure_opts=()
  _configure_opts+=(
    --sysconfdir="/etc"
    --prefix="/usr"
    --enable-startup-notification
    --enable-session
    --enable-alt-input-wins
  )
  if [[ "${_gconf}" == "true" ]]; then
    _configure_opts+=(
      --enable-gconf
    )
  elif [[ "${_gconf}" == "false" ]]; then
    _configure_opts+=(
      --disable-gconf
    )
  fi
  if [[ "${_expat}" == "true" ]]; then
    _configure_opts+=(
      --enable-expat
    )
  elif [[ "${_expat}" == "false" ]]; then
    _configure_opts+=(
      --disable-expat
    )
  fi
  _cflags+=(
    $CFLAGS
    -fcommon
  )
  if [[ "${_os}" == "Android" ]]; then
    _cflags+=(
      -Wl,--allow-shlib-undefined
    )
  fi
  export \
    CFLAGS="${_cflags[*]}"
  cd \
    "${_tarname}"
  CFLAGS="${_cflags[*]}" \
  ./autogen.sh
  CFLAGS="${_cflags[*]}" \
  ./configure \
    "${_configure_opts[@]}"
  CFLAGS="${_cflags[*]}" \
  make
}

package() {
  cd \
    "${_tarname}"
  make \
    DESTDIR="${pkgdir}" \
    install
}
