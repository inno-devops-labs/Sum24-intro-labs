## Lab 4 Report 
Kirill Glinskiy k.glinsky@innopolis.university TG: @amrtized
#### Task 1
First i made a separate directory for a local repo:

```shell
mkdir -p ~/local-apt-repo
```

Then i copied .deb file to local apt repo folder. In my case it's AnyDesk app:

```shell
cp anydesk_6.3.2-1_amd64.deb  ~/local-apt-repo/
```

Then i used dpkg-scanpackages to create a Packages file + compressed into a .gz archive:

```shell
dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
```
```shell
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   anydesk
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
```

Then I added repo to the sources:

```shell
echo "deb [trusted=yes] file:/home/yourusername/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
```

And analized the content of Packages.gz:

```
zcat Packages.gz
Package: anydesk
Version: 6.3.2
Architecture: amd64
Maintainer: AnyDesk Software GmbH <linux-support@anydesk.com>
Installed-Size: 16794
Depends: libc6 (>= 2.7), libgcc1 (>= 1:4.1.1), libglib2.0-0 (>= 2.16.0), libgtk2.0-0 (>= 2.20.1), libstdc++6 (>= 4.1.1), libx11-6, libxcb-shm0, libxcb1, libpango-1.0-0, libcairo2, libxrandr2 (>= 1.3), libx11-xcb1, libxtst6, libxfixes3, libxdamage1, libxkbfile1, libgtkglext1
Recommends: libglx-mesa0, xdg-utils
Filename: /home/slam/local-apt-repo/anydesk_6.3.2-1_amd64.deb
Size: 7022112
MD5sum: 264cd9916cf922502edaeb788b4d0f3d
SHA1: bc5df948ffcd5b73b5f92c5fd718335795eacedc
SHA256: 2bc739676672b531e91d50f302c6ea8ad6b1612dc499d1d2f83b21a4c852658d
Section: net
Priority: optional
Homepage: https://anydesk.com/
Description: The fastest remote desktop software on the market.
  It allows for new usage scenarios and applications that have not been possible with current remote desktop software.
```
As we can see the repo is indeed the local one inside of /home/slam/local-apt-repo .

With  apt policy anydesk i can see the candidate for installation and its policy.

It shows that it is already installed - and it is logical - because I've already installed one before.
```
anydesk:
  Installed: 6.3.2
  Candidate: 6.3.2
  Version table:
 *** 6.3.2 100
        100 /var/lib/dpkg/status
```

And, I can install it if I want to. 
```
 sudo apt install anydesk
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
anydesk is already the newest version (6.3.2).
The following packages were automatically installed and are no longer required:
  libappstream-glib8 libatomic1:i386 libdrm-amdgpu1:i386 libdrm-intel1:i386
  libdrm-nouveau2:i386 libdrm-radeon1:i386 libdrm2:i386 libedit2:i386
  libelf1:i386 libexpat1:i386 libffi8:i386 libgl1:i386 libgl1-mesa-dri:i386
  libglapi-mesa:i386 libglvnd0:i386 libglx-mesa0:i386 libglx0:i386
  libicu70:i386 libllvm15:i386 libpciaccess0:i386 libsensors5:i386
  libstdc++6:i386 libwpe-1.0-1 libwpebackend-fdo-1.0-1 libx11-xcb1:i386
  libxcb-dri2-0:i386 libxcb-dri3-0:i386 libxcb-glx0:i386 libxcb-present0:i386
  libxcb-randr0:i386 libxcb-shm0:i386 libxcb-sync1:i386 libxcb-xfixes0:i386
  libxfixes3:i386 libxml2:i386 libxshmfence1:i386 libxxf86vm1:i386
  nvidia-firmware-535-535.154.05 nvidia-firmware-535-535.171.04
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 143 not upgraded.
```

#### Task 2
Let's try to imitate marble package installation. Here we can see that it exists, and availible for ubuntu users.
```
apt-cache showpkg marble
Package: marble
Versions: 
4:21.12.3-0ubuntu1 (/var/lib/apt/lists/ru.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages)
 Description Language: 
                 File: /var/lib/apt/lists/ru.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
                  MD5: 1f126a4752fd8384e6c2471b34c0cba7
 Description Language: en
                 File: /var/lib/apt/lists/ru.archive.ubuntu.com_ubuntu_dists_jammy_universe_i18n_Translation-en
                  MD5: 1f126a4752fd8384e6c2471b34c0cba7


Reverse Depends: 
  kdeedu,marble 4:21.08.0
  plasma-marble,marble 4:17.08.3-3~
  plasma-marble,marble 4:17.08.3-3~
  gis-gps,marble
Dependencies: 
4:21.12.3-0ubuntu1 - marble-data (2 4:21.12.3-0ubuntu1) marble-plugins (5 4:21.12.3-0ubuntu1) kio (0 (null)) libc6 (2 2.34) libgcc-s1 (2 3.0) libkf5configcore5 (2 4.98.0) libkf5configgui5 (2 4.97.0) libkf5configwidgets5 (2 4.96.0) libkf5coreaddons5 (2 5.7.0~) libkf5crash5 (2 5.7.0~) libkf5i18n5 (2 5.7.0~) libkf5kiowidgets5 (2 5.7.0~) libkf5parts5 (2 5.7.0~) libkf5widgetsaddons5 (2 4.96.0) libkf5xmlgui5 (2 4.98.0) libmarblewidget-qt5-28 (5 4:21.12.3-0ubuntu1) libqt5core5a (2 5.15.1) libqt5dbus5 (2 5.7.0~) libqt5gui5 (18 5.7.0) libqt5gui5-gles (2 5.7.0) libqt5network5 (2 5.7.0~) libqt5printsupport5 (2 5.7.0~) libqt5widgets5 (2 5.7.0~) libqt5xml5 (2 5.7.0~) libstdc++6 (2 4.1.1) marble-data (3 4:17.08.1) gosmore (0 (null)) monav-routing-daemon (0 (null)) routino (0 (null)) marble-data (3 4:17.08.1) 
Provides: 
4:21.12.3-0ubuntu1 - 
Reverse Provides:

```
Now, let's simulate the installation with the -s flag. First batch of additional packages to be installed can be found after the line:

*The following additional packages will be installed:*

Dependencies can be found with apt-cache showpkg after line:

*Dependencies:*



```sudo apt-get install -s marble
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libappstream-glib8 libatomic1:i386 libdrm-amdgpu1:i386 libdrm-intel1:i386
  libdrm-nouveau2:i386 libdrm-radeon1:i386 libdrm2:i386 libedit2:i386
  libelf1:i386 libexpat1:i386 libffi8:i386 libgl1:i386 libgl1-mesa-dri:i386
  libglapi-mesa:i386 libglvnd0:i386 libglx-mesa0:i386 libglx0:i386
  libicu70:i386 libllvm15:i386 libpciaccess0:i386 libsensors5:i386
  libstdc++6:i386 libwpe-1.0-1 libwpebackend-fdo-1.0-1 libx11-xcb1:i386
  libxcb-dri2-0:i386 libxcb-dri3-0:i386 libxcb-glx0:i386 libxcb-present0:i386
  libxcb-randr0:i386 libxcb-shm0:i386 libxcb-sync1:i386 libxcb-xfixes0:i386
  libxfixes3:i386 libxml2:i386 libxshmfence1:i386 libxxf86vm1:i386
  nvidia-firmware-535-535.154.05 nvidia-firmware-535-535.171.04
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  gamin kded5 kio kwayland-data kwayland-integration libaribb24-0 libastro1
  libcddb2 libdbusmenu-qt5-2 libdca0 libdvbpsi10 libdvdnav4 libebml5 libfaad2
  libgamin0 libgps28 libhfstospell11 libixml10 libkate1 libkf5archive5
  libkf5auth-data libkf5authcore5 libkf5codecs-data libkf5codecs5
  libkf5completion-data libkf5completion5 libkf5config-bin libkf5config-data
  libkf5configcore5 libkf5configgui5 libkf5configwidgets-data
  libkf5configwidgets5 libkf5coreaddons-data libkf5coreaddons5 libkf5crash5
  libkf5dbusaddons-bin libkf5dbusaddons-data libkf5dbusaddons5 libkf5doctools5
  libkf5globalaccel-bin libkf5globalaccel-data libkf5globalaccel5
  libkf5globalaccelprivate5 libkf5guiaddons-bin libkf5guiaddons-data
  libkf5guiaddons5 libkf5i18n-data libkf5i18n5 libkf5iconthemes-bin
  libkf5iconthemes-data libkf5iconthemes5 libkf5idletime5 libkf5itemviews-data
  libkf5itemviews5 libkf5jobwidgets-data libkf5jobwidgets5 libkf5kiocore5
  libkf5kiogui5 libkf5kiontlm5 libkf5kiowidgets5 libkf5notifications-data
  libkf5notifications5 libkf5parts-data libkf5parts-plugins libkf5parts5
  libkf5service-bin libkf5service-data libkf5service5 libkf5solid5
  libkf5solid5-data libkf5sonnet5-data libkf5sonnetcore5 libkf5sonnetui5
  libkf5textwidgets-data libkf5textwidgets5 libkf5wallet-bin libkf5wallet-data
  libkf5wallet5 libkf5waylandclient5 libkf5widgetsaddons-data
  libkf5widgetsaddons5 libkf5windowsystem-data libkf5windowsystem5
  libkf5xmlgui-bin libkf5xmlgui-data libkf5xmlgui5 libkwalletbackend5-5
  liblua5.2-0 libmad0 libmarblewidget-qt5-28 libmatroska7 libmpcdec6
  libopenmpt-modplug1 libphonon4qt5-4 libphonon4qt5-data libplacebo192
  libpolkit-qt5-1-1 libprotobuf-lite23 libproxy-tools libqt5serialport5
  libqt5texttospeech5 libqt5waylandclient5 libqt5waylandcompositor5
  libqt5webengine-data libqt5webenginecore5 libqt5webenginewidgets5
  libqt5x11extras5 libre2-9 libresid-builder0c2a libsdl-image1.2
  libsdl1.2debian libshp2 libsidplay2 libspatialaudio0 libssh2-1 libupnp13
  libvlc-bin libvlc5 libvlccore9 libvoikko1 marble-data marble-plugins
  marble-qt-data phonon4qt5 phonon4qt5-backend-vlc qtspeech5-speechd-plugin
  qtwayland5 sonnet-plugins vlc-data vlc-plugin-base vlc-plugin-video-output
Suggested packages:
  libdvdcss2 gpsd voikko-fi gosmore monav-routing-daemon routino
  phonon4qt5-backend-gstreamer hspell
The following NEW packages will be installed:
  gamin kded5 kio kwayland-data kwayland-integration libaribb24-0 libastro1
  libcddb2 libdbusmenu-qt5-2 libdca0 libdvbpsi10 libdvdnav4 libebml5 libfaad2
  libgamin0 libgps28 libhfstospell11 libixml10 libkate1 libkf5archive5
  libkf5auth-data libkf5authcore5 libkf5codecs-data libkf5codecs5
  libkf5completion-data libkf5completion5 libkf5config-bin libkf5config-data
  libkf5configcore5 libkf5configgui5 libkf5configwidgets-data
  libkf5configwidgets5 libkf5coreaddons-data libkf5coreaddons5 libkf5crash5
  libkf5dbusaddons-bin libkf5dbusaddons-data libkf5dbusaddons5 libkf5doctools5
  libkf5globalaccel-bin libkf5globalaccel-data libkf5globalaccel5
  libkf5globalaccelprivate5 libkf5guiaddons-bin libkf5guiaddons-data
  libkf5guiaddons5 libkf5i18n-data libkf5i18n5 libkf5iconthemes-bin
  libkf5iconthemes-data libkf5iconthemes5 libkf5idletime5 libkf5itemviews-data
  libkf5itemviews5 libkf5jobwidgets-data libkf5jobwidgets5 libkf5kiocore5
  libkf5kiogui5 libkf5kiontlm5 libkf5kiowidgets5 libkf5notifications-data
  libkf5notifications5 libkf5parts-data libkf5parts-plugins libkf5parts5
  libkf5service-bin libkf5service-data libkf5service5 libkf5solid5
  libkf5solid5-data libkf5sonnet5-data libkf5sonnetcore5 libkf5sonnetui5
  libkf5textwidgets-data libkf5textwidgets5 libkf5wallet-bin libkf5wallet-data
  libkf5wallet5 libkf5waylandclient5 libkf5widgetsaddons-data
  libkf5widgetsaddons5 libkf5windowsystem-data libkf5windowsystem5
  libkf5xmlgui-bin libkf5xmlgui-data libkf5xmlgui5 libkwalletbackend5-5
  liblua5.2-0 libmad0 libmarblewidget-qt5-28 libmatroska7 libmpcdec6
  libopenmpt-modplug1 libphonon4qt5-4 libphonon4qt5-data libplacebo192
  libpolkit-qt5-1-1 libprotobuf-lite23 libproxy-tools libqt5serialport5
  libqt5texttospeech5 libqt5waylandclient5 libqt5waylandcompositor5
  libqt5webengine-data libqt5webenginecore5 libqt5webenginewidgets5
  libqt5x11extras5 libre2-9 libresid-builder0c2a libsdl-image1.2
  libsdl1.2debian libshp2 libsidplay2 libspatialaudio0 libssh2-1 libupnp13
  libvlc-bin libvlc5 libvlccore9 libvoikko1 marble marble-data marble-plugins
  marble-qt-data phonon4qt5 phonon4qt5-backend-vlc qtspeech5-speechd-plugin
  qtwayland5 sonnet-plugins vlc-data vlc-plugin-base vlc-plugin-video-output
0 upgraded, 132 newly installed, 0 to remove and 143 not upgraded.
Inst libgamin0 (0.1.10-6 Ubuntu:22.04/jammy [amd64]) []
Inst gamin (0.1.10-6 Ubuntu:22.04/jammy [amd64])
Inst libkf5config-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5configcore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5coreaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5coreaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5windowsystem-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libqt5x11extras5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst libkf5windowsystem5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5crash5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5dbusaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5dbusaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5i18n-data (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [all])
Inst libkf5i18n5 (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libkf5service-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5service5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5service-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst kded5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5archive5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5auth-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libpolkit-qt5-1-1 (0.114.0-2 Ubuntu:22.04/jammy [amd64])
Inst libkf5authcore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5codecs-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5codecs5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5configwidgets-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5configgui5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5guiaddons-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5guiaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libqt5waylandclient5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst libkf5guiaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5widgetsaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5widgetsaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5configwidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5doctools5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5itemviews-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5itemviews5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5kiocore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5kiogui5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5kiontlm5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5completion-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5completion5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5iconthemes-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5iconthemes5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5jobwidgets-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5jobwidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5solid5-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5solid5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5kiowidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5notifications-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libdbusmenu-qt5-2 (0.9.3+16.04.20160218-2build1 Ubuntu:22.04/jammy [amd64])
Inst libqt5texttospeech5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst libkf5notifications5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5textwidgets-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5sonnet5-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5sonnetcore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5sonnetui5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5textwidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5wallet-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkwalletbackend5-5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5wallet5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5wallet-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst kio (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst kwayland-data (4:5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5idletime5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5waylandclient5 (4:5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst kwayland-integration (4:5.24.4-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libaribb24-0 (1.0.3-2 Ubuntu:22.04/jammy [amd64])
Inst libastro1 (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libcddb2 (1.3.2-7fakesync1 Ubuntu:22.04/jammy [amd64])
Inst libdvbpsi10 (1.3.3-1 Ubuntu:22.04/jammy [amd64])
Inst libdvdnav4 (6.1.1-1 Ubuntu:22.04/jammy [amd64])
Inst libebml5 (1.4.2-2 Ubuntu:22.04/jammy [amd64])
Inst libfaad2 (2.10.0-2 Ubuntu:22.04/jammy [amd64])
Inst libgps28 (3.22-4ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libhfstospell11 (0.5.2-1build3 Ubuntu:22.04/jammy [amd64])
Inst libixml10 (1:1.8.4-2ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libkate1 (0.4.1-11build1 Ubuntu:22.04/jammy [amd64])
Inst libkf5config-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5dbusaddons-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5globalaccel-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5globalaccel5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5globalaccelprivate5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5globalaccel-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5iconthemes-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5parts-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libkf5xmlgui-data (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [all])
Inst libkf5xmlgui5 (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libkf5parts5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5parts-plugins (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libkf5xmlgui-bin (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst liblua5.2-0 (5.2.4-2 Ubuntu:22.04/jammy [amd64])
Inst libmad0 (0.15.1b-10ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst marble-qt-data (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst libphonon4qt5-data (4:4.11.1-4 Ubuntu:22.04/jammy [all])
Inst libphonon4qt5-4 (4:4.11.1-4 Ubuntu:22.04/jammy [amd64])
Inst libqt5webengine-data (5.15.9+dfsg-1 Ubuntu:22.04/jammy [all])
Inst libre2-9 (20220201+dfsg-1 Ubuntu:22.04/jammy [amd64])
Inst libqt5webenginecore5 (5.15.9+dfsg-1 Ubuntu:22.04/jammy [amd64])
Inst libqt5webenginewidgets5 (5.15.9+dfsg-1 Ubuntu:22.04/jammy [amd64])
Inst vlc-data (3.0.16-1build7 Ubuntu:22.04/jammy [all])
Inst libdca0 (0.0.7-2 Ubuntu:22.04/jammy [amd64])
Inst libmatroska7 (1.6.3-2 Ubuntu:22.04/jammy [amd64])
Inst libmpcdec6 (2:0.1~r495-2 Ubuntu:22.04/jammy [amd64])
Inst libopenmpt-modplug1 (0.8.9.0-openmpt1-2 Ubuntu:22.04/jammy [amd64])
Inst libprotobuf-lite23 (3.12.4-1ubuntu7.22.04.1 Ubuntu:22.04/jammy-updates, Ubuntu:22.04/jammy-security [amd64])
Inst libresid-builder0c2a (2.1.1-15ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libsdl1.2debian (1.2.15+dfsg2-6 Ubuntu:22.04/jammy [amd64])
Inst libsdl-image1.2 (1.2.12-13build1 Ubuntu:22.04/jammy [amd64])
Inst libsidplay2 (2.1.1-15ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libspatialaudio0 (0.3.0+git20180730+dfsg1-2build1 Ubuntu:22.04/jammy [amd64])
Inst libssh2-1 (1.10.0-3 Ubuntu:22.04/jammy [amd64])
Inst libupnp13 (1:1.8.4-2ubuntu2 Ubuntu:22.04/jammy [amd64])
Inst libvlccore9 (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Inst vlc-plugin-base (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Inst libplacebo192 (4.192.1-1 Ubuntu:22.04/jammy [amd64])
Inst vlc-plugin-video-output (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Inst libvlc5 (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Inst phonon4qt5-backend-vlc (0.11.3-1 Ubuntu:22.04/jammy [amd64])
Inst phonon4qt5 (4:4.11.1-4 Ubuntu:22.04/jammy [amd64])
Inst libmarblewidget-qt5-28 (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst libproxy-tools (0.4.17-2 Ubuntu:22.04/jammy [amd64])
Inst libqt5serialport5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst libqt5waylandcompositor5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst libshp2 (1.5.0-2 Ubuntu:22.04/jammy [amd64])
Inst libvlc-bin (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Inst libvoikko1 (4.3.1-1build1 Ubuntu:22.04/jammy [amd64])
Inst marble-data (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [all])
Inst marble-plugins (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst marble (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst qtspeech5-speechd-plugin (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst qtwayland5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Inst sonnet-plugins (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libgamin0 (0.1.10-6 Ubuntu:22.04/jammy [amd64])
Conf gamin (0.1.10-6 Ubuntu:22.04/jammy [amd64])
Conf libkf5config-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5configcore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5coreaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5coreaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5windowsystem-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libqt5x11extras5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf libkf5windowsystem5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5crash5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5dbusaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5dbusaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5i18n-data (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [all])
Conf libkf5i18n5 (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libkf5service-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5service5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5service-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf kded5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5archive5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5auth-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libpolkit-qt5-1-1 (0.114.0-2 Ubuntu:22.04/jammy [amd64])
Conf libkf5authcore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5codecs-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5codecs5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5configwidgets-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5configgui5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5guiaddons-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5guiaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libqt5waylandclient5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf libkf5guiaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5widgetsaddons-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5widgetsaddons5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5configwidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5doctools5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5itemviews-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5itemviews5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5kiocore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5kiogui5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5kiontlm5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5completion-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5completion5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5iconthemes-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5iconthemes5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5jobwidgets-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5jobwidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5solid5-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5solid5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5kiowidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5notifications-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libdbusmenu-qt5-2 (0.9.3+16.04.20160218-2build1 Ubuntu:22.04/jammy [amd64])
Conf libqt5texttospeech5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf libkf5notifications5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5textwidgets-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5sonnet5-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5sonnetcore5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5sonnetui5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5textwidgets5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5wallet-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkwalletbackend5-5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5wallet5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5wallet-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf kio (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf kwayland-data (4:5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5idletime5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5waylandclient5 (4:5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf kwayland-integration (4:5.24.4-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libaribb24-0 (1.0.3-2 Ubuntu:22.04/jammy [amd64])
Conf libastro1 (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libcddb2 (1.3.2-7fakesync1 Ubuntu:22.04/jammy [amd64])
Conf libdvbpsi10 (1.3.3-1 Ubuntu:22.04/jammy [amd64])
Conf libdvdnav4 (6.1.1-1 Ubuntu:22.04/jammy [amd64])
Conf libebml5 (1.4.2-2 Ubuntu:22.04/jammy [amd64])
Conf libfaad2 (2.10.0-2 Ubuntu:22.04/jammy [amd64])
Conf libgps28 (3.22-4ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libhfstospell11 (0.5.2-1build3 Ubuntu:22.04/jammy [amd64])
Conf libixml10 (1:1.8.4-2ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libkate1 (0.4.1-11build1 Ubuntu:22.04/jammy [amd64])
Conf libkf5config-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5dbusaddons-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5globalaccel-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5globalaccel5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5globalaccelprivate5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5globalaccel-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5iconthemes-bin (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5parts-data (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libkf5xmlgui-data (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [all])
Conf libkf5xmlgui5 (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libkf5parts5 (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5parts-plugins (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libkf5xmlgui-bin (5.92.0-0ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf liblua5.2-0 (5.2.4-2 Ubuntu:22.04/jammy [amd64])
Conf libmad0 (0.15.1b-10ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf marble-qt-data (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf libphonon4qt5-data (4:4.11.1-4 Ubuntu:22.04/jammy [all])
Conf libphonon4qt5-4 (4:4.11.1-4 Ubuntu:22.04/jammy [amd64])
Conf libqt5webengine-data (5.15.9+dfsg-1 Ubuntu:22.04/jammy [all])
Conf libre2-9 (20220201+dfsg-1 Ubuntu:22.04/jammy [amd64])
Conf libqt5webenginecore5 (5.15.9+dfsg-1 Ubuntu:22.04/jammy [amd64])
Conf libqt5webenginewidgets5 (5.15.9+dfsg-1 Ubuntu:22.04/jammy [amd64])
Conf vlc-data (3.0.16-1build7 Ubuntu:22.04/jammy [all])
Conf libdca0 (0.0.7-2 Ubuntu:22.04/jammy [amd64])
Conf libmatroska7 (1.6.3-2 Ubuntu:22.04/jammy [amd64])
Conf libmpcdec6 (2:0.1~r495-2 Ubuntu:22.04/jammy [amd64])
Conf libopenmpt-modplug1 (0.8.9.0-openmpt1-2 Ubuntu:22.04/jammy [amd64])
Conf libprotobuf-lite23 (3.12.4-1ubuntu7.22.04.1 Ubuntu:22.04/jammy-updates, Ubuntu:22.04/jammy-security [amd64])
Conf libresid-builder0c2a (2.1.1-15ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libsdl1.2debian (1.2.15+dfsg2-6 Ubuntu:22.04/jammy [amd64])
Conf libsdl-image1.2 (1.2.12-13build1 Ubuntu:22.04/jammy [amd64])
Conf libsidplay2 (2.1.1-15ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libspatialaudio0 (0.3.0+git20180730+dfsg1-2build1 Ubuntu:22.04/jammy [amd64])
Conf libssh2-1 (1.10.0-3 Ubuntu:22.04/jammy [amd64])
Conf libupnp13 (1:1.8.4-2ubuntu2 Ubuntu:22.04/jammy [amd64])
Conf libvlccore9 (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Conf vlc-plugin-base (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Conf libplacebo192 (4.192.1-1 Ubuntu:22.04/jammy [amd64])
Conf vlc-plugin-video-output (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Conf libvlc5 (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Conf phonon4qt5-backend-vlc (0.11.3-1 Ubuntu:22.04/jammy [amd64])
Conf phonon4qt5 (4:4.11.1-4 Ubuntu:22.04/jammy [amd64])
Conf libmarblewidget-qt5-28 (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf libproxy-tools (0.4.17-2 Ubuntu:22.04/jammy [amd64])
Conf libqt5serialport5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf libqt5waylandcompositor5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf libshp2 (1.5.0-2 Ubuntu:22.04/jammy [amd64])
Conf libvlc-bin (3.0.16-1build7 Ubuntu:22.04/jammy [amd64])
Conf libvoikko1 (4.3.1-1build1 Ubuntu:22.04/jammy [amd64])
Conf marble-data (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [all])
Conf marble-plugins (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf marble (4:21.12.3-0ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf qtspeech5-speechd-plugin (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf qtwayland5 (5.15.3-1 Ubuntu:22.04/jammy [amd64])
Conf sonnet-plugins (5.92.0-0ubuntu1 Ubuntu:22.04/jammy [amd64])
```

#### Task 3

First, I installed a tool to read xml files from .cpp:

```shell
sudo apt install libpugixml-dev
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libappstream-glib8 libatomic1:i386 libdrm-amdgpu1:i386 libdrm-intel1:i386
  libdrm-nouveau2:i386 libdrm-radeon1:i386 libdrm2:i386 libedit2:i386
  libelf1:i386 libexpat1:i386 libffi8:i386 libgl1:i386 libgl1-mesa-dri:i386
  libglapi-mesa:i386 libglvnd0:i386 libglx-mesa0:i386 libglx0:i386
  libicu70:i386 libllvm15:i386 libpciaccess0:i386 libsensors5:i386
  libstdc++6:i386 libwpe-1.0-1 libwpebackend-fdo-1.0-1 libx11-xcb1:i386
  libxcb-dri2-0:i386 libxcb-dri3-0:i386 libxcb-glx0:i386 libxcb-present0:i386
  libxcb-randr0:i386 libxcb-shm0:i386 libxcb-sync1:i386 libxcb-xfixes0:i386
  libxfixes3:i386 libxml2:i386 libxshmfence1:i386 libxxf86vm1:i386
  nvidia-firmware-535-535.154.05 nvidia-firmware-535-535.171.04
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  libpugixml-dev
0 upgraded, 1 newly installed, 0 to remove and 143 not upgraded.
Need to get 114 kB of archives.
After this operation, 507 kB of additional disk space will be used.
Get:1 http://ru.archive.ubuntu.com/ubuntu jammy/universe amd64 libpugixml-dev amd64 1.12.1-1 [114 kB]
Fetched 114 kB in 0s (529 kB/s)        
Selecting previously unselected package libpugixml-dev:amd64.
(Reading database ... 318486 files and directories currently installed.)
Preparing to unpack .../libpugixml-dev_1.12.1-1_amd64.deb ...
Unpacking libpugixml-dev:amd64 (1.12.1-1) ...
Setting up libpugixml-dev:amd64 (1.12.1-1) ...
```

Then, I held the package to not allow upgrades:

```shell
sudo apt-mark hold libpugixml-dev
libpugixml-dev set on hold.
```
We can see that this is the only package which is holding now.
```
apt-mark showhold
libpugixml-dev
```
We can also unhold it, so it can be updated later if requested:

```
sudo apt-mark unhold libpugixml-dev
Canceled hold on libpugixml-dev.
```