# Maintainer: Alan Jenkins <alan.james.jenkins [at] gmail.com>
# Original wolf-data package by M0Rf30
pkgname=wolf-data-steam
pkgver=1.41b
pkgrel=3
pkgdesc="Return to Castle Wolfenstein native Linux Single Player data via Steam"
arch=('any')
conflicts=('wolf-data')
provides=('wolf-data')
depends=('steamcmd')
url="ftp://ftp.internat.freebsd.org/pub/FreeBSD/distfiles/"
license=('GPL')
install='wolf-data-steam.install'
source=("https://dl.dropboxusercontent.com/s/97qyelre9iryv37/wolf-linux-${pkgver}.x86.run")
md5sums=('2aa37968aff19d665ed6c001773b2de3')

package() {
    # Set Install Files to Executable
    cd $srcdir
    chmod +x wolf-linux-${pkgver}.x86.run

    # Extract Linux Game Files
    ./wolf-linux-${pkgver}.x86.run --target files --noexec
    cd files
    # Remove Unneeded Files and Directories
    cd main
    rm *.so

    # Move Data to Package Directory
    mkdir -p $pkgdir/opt/wolf-data
    cp -r * $pkgdir/opt/wolf-data/

    # Use steamcmd to get the rest of the data required.
    mkdir -p $srcdir/wolf-data-steam
    printf "Enter your Steam username:"
    read steam_username
    steamcmd +@sSteamCmdForcePlatformType windows +@ShutdownOnFailedCommand 1 +force_install_dir $srcdir/wolf-data-steam +login $steam_username "+app_update 9010 validate" +quit

    # Move required files to pkgdir
    install -D -m 644 $srcdir/wolf-data-steam/Main/pak0.pk3 $pkgdir/
    install -D -m 644 $srcdir/wolf-data-steam/Main/sp_pak1.pk3 $pkgdir/
    install -D -m 644 $srcdir/wolf-data-steam/Main/mp_pak0.pk3 $pkgdir/
}

