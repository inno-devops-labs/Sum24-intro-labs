## Task 1: Configure and Use a Local Package Repository

__1. Create a Local Repository:__
```sh
mkdir -p ~/local-apt-repo
cp Desktop/audacity_2.4.2~dfsg0-5_amd64.deb ~/local-apt-repo/

```
__2. Generate the Package Index:__
```sh
dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz

dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   audacity
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.


```
__3. Add the repository to your sources.list.__

```sh
echo "deb [trusted=yes] file:/home/applewolf/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
sudo apt update

deb [trusted=yes] file:/home/applewolf/local-apt-repo ./
```
__4. Verify the Contents of the Packages.gz File:__

```sh

zcat Packages.gz

Package: audacity
Version: 2.4.2~dfsg0-5
Architecture: amd64
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Installed-Size: 16128
Depends: audacity-data (= 2.4.2~dfsg0-5), libavcodec58 (>= 7:4.0), libavformat58 (>= 7:4.2), libavutil56 (>= 7:4.0), libc6 (>= 2.33), libexpat1 (>= 2.0.1), libflac++6v5 (>= 1.3.1), libflac8 (>= 1.3.0), libgcc-s1 (>= 3.3.1), libgdk-pixbuf-2.0-0 (>= 2.22.0), libglib2.0-0 (>= 2.12.0), libgtk-3-0 (>= 3.9.10), libid3tag0 (>= 0.15.1b), liblilv-0-0 (>= 0.24.0~dfsg0), libmad0 (>= 0.15.1b-3), libogg0 (>= 1.0rc3), libportaudio2 (>= 19+svn20101113), libportsmf0v5, libsndfile1 (>= 1.0.20), libsoundtouch1 (>= 2.0.0), libsoxr0 (>= 0.1.1), libstdc++6 (>= 6), libsuil-0-0 (>= 0.8.0~dfsg0), libtwolame0 (>= 0.3.6), libvamp-hostsdk3v5 (>= 2.10.0), libvorbis0a (>= 1.3.3), libvorbisenc2 (>= 1.3.3), libvorbisfile3 (>= 1.3.3), libwxbase3.0-0v5 (>= 3.0.5.1+dfsg), libwxgtk3.0-gtk3-0v5 (>= 3.0.5.1+dfsg)
Suggests: ladspa-plugin
Filename: /home/applewolf/local-apt-repo/audacity_2.4.2~dfsg0-5_amd64.deb
Size: 4190852
MD5sum: d96966fc1f0feb9a77fe631dfb827937
SHA1: 13d556647ce36387be4b1e976700a397d850dce8
SHA256: 6e9da0a893a1019d5198ea931d701851dfc1390675a6575451feae93ea083575
Section: sound
Priority: optional
Homepage: https://www.audacityteam.org/
Description: fast, cross-platform audio editor
 Audacity is a multi-track audio editor for Linux/Unix, MacOS and
 Windows.  It is designed for easy recording, playing and editing of
 digital audio.  Audacity features digital effects and spectrum
 analysis tools.  Editing is very fast and provides unlimited
 undo/redo.


apt policy audacity

audacity:
  Installed: (none)
  Candidate: 2.4.2~dfsg0-5
  Version table:
     2.4.2~dfsg0-5 500
        500 http://mirror.hoztnode.net/ubuntu jammy/universe amd64 Packages

```
__5. Install a package using apt from your local repository.__
```sh
sudo apt install audacity

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  adwaita-icon-theme alsa-topology-conf alsa-ucm-conf at-spi2-core audacity-data dconf-gsettings-backend
  dconf-service fontconfig gsettings-desktop-schemas gtk-update-icon-cache hicolor-icon-theme humanity-icon-theme
  i965-va-driver intel-media-va-driver libaacs0 libaom3 libasound2 libasound2-data libatk-bridge2.0-0 libatk1.0-0
  libatk1.0-data libatspi2.0-0 libavahi-client3 libavahi-common-data libavahi-common3 libavcodec58 libavformat58
  libavutil56 libbdplus0 libbluray2 libcairo-gobject2 libcairo2 libchromaprint1 libcodec2-1.0 libcolord2 libcups2
  libdatrie1 libdav1d5 libdconf1 libdouble-conversion3 libdrm-amdgpu1 libdrm-intel1 libdrm-nouveau2
  libdrm-radeon1 libegl-mesa0 libegl1 libepoxy0 libflac++6v5 libflac8 libfribidi0 libgail-common libgail18
  libgbm1 libgdk-pixbuf-2.0-0 libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgl1 libgl1-amber-dri
  libgl1-mesa-dri libglapi-mesa libglvnd0 libglx-mesa0 libglx0 libgme0 libgraphite2-3 libgsm1 libgtk-3-0
  libgtk-3-bin libgtk-3-common libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libharfbuzz0b libice6 libid3tag0
  libigdgmm12 libinput-bin libinput10 libjack-jackd2-0 liblcms2-2 liblilv-0-0 libllvm15 libmad0 libmd4c0 libmfx1
  libmp3lame0 libmpg123-0 libmtdev1 libnorm1 libnotify4 libnuma1 libogg0 libopenjp2-7 libopenmpt0 libopus0
  libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpciaccess0 libpcre2-16-0 libpgm-5.3-0 libpixman-1-0
  libportaudio2 libportsmf0v5 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5svg5 libqt5widgets5
  libqt5x11extras5 librabbitmq4 librsvg2-2 librsvg2-common libsamplerate0 libsensors-config libsensors5
  libserd-0-0 libshine3 libsm6 libsnappy1v5 libsndfile1 libsodium23 libsord-0-0 libsoundtouch1 libsoxr0 libspeex1
  libsratom-0-0 libsrt1.4-gnutls libssh-gcrypt-4 libsuil-0-0 libswresample3 libthai-data libthai0 libtheora0
  libtwolame0 libudfread0 libva-drm2 libva-x11-2 libva2 libvamp-hostsdk3v5 libvdpau1 libvorbis0a libvorbisenc2
  libvorbisfile3 libvpx7 libwacom-bin libwacom-common libwacom9 libwayland-client0 libwayland-cursor0
  libwayland-egl1 libwayland-server0 libwebpmux3 libwxbase3.0-0v5 libwxgtk3.0-gtk3-0v5 libx11-xcb1 libx264-163
  libx265-199 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-present0
  libxcb-randr0 libxcb-render-util0 libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-util1
  libxcb-xfixes0 libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxcomposite1 libxcursor1 libxdamage1 libxfixes3
  libxi6 libxinerama1 libxkbcommon-x11-0 libxkbcommon0 libxrandr2 libxrender1 libxshmfence1 libxtst6 libxvidcore4
  libxxf86vm1 libzmq5 libzvbi-common libzvbi0 mesa-va-drivers mesa-vdpau-drivers ocl-icd-libopencl1
  qt5-gtk-platformtheme qttranslations5-l10n session-migration ubuntu-mono va-driver-all vdpau-driver-all
  x11-common
  ...
```

## Task 2: Simulate Package Installation and Identify Dependencies

__1.Choose a Package to Simulate:__
```sh
apt-cache showpkg audacity

Package: audacity
Versions:
2.4.2~dfsg0-5 (/var/lib/apt/lists/mirror.hoztnode.net_ubuntu_dists_jammy_universe_binary-amd64_Packages) (/var/lib/dpkg/status)
 Description Language:
                 File: /var/lib/apt/lists/mirror.hoztnode.net_ubuntu_dists_jammy_universe_binary-amd64_Packages
                  MD5: f3049c5343ef448931624eb10a0c6627
 Description Language: en
                 File: /var/lib/apt/lists/mirror.hoztnode.net_ubuntu_dists_jammy_universe_i18n_Translation-en
                  MD5: f3049c5343ef448931624eb10a0c6627


Reverse Depends:
  audacity-data,audacity
  ubuntustudio-video,audacity
  ubuntustudio-audio,audacity
  ubuntustudio-video,audacity
  ubuntustudio-audio,audacity
  tucnak,audacity
  multimedia-recording,audacity
  multimedia-mixing,audacity
  multimedia-audio-utilities,audacity
  jacktrip-gui,audacity
  games-content-dev,audacity
  forensics-extra-gui,audacity
Dependencies:
2.4.2~dfsg0-5 - audacity-data (5 2.4.2~dfsg0-5) libavcodec58 (2 7:4.0) libavformat58 (2 7:4.2) libavutil56 (2 7:4.0) libc6 (2 2.33) libexpat1 (2 2.0.1) libflac++6v5 (2 1.3.1) libflac8 (2 1.3.0) libgcc-s1 (2 3.3.1) libgdk-pixbuf-2.0-0 (2 2.22.0) libglib2.0-0 (2 2.12.0) libgtk-3-0 (2 3.9.10) libid3tag0 (2 0.15.1b) liblilv-0-0 (2 0.24.0~dfsg0) libmad0 (2 0.15.1b-3) libogg0 (2 1.0rc3) libportaudio2 (2 19+svn20101113) libportsmf0v5 (0 (null)) libsndfile1 (2 1.0.20) libsoundtouch1 (2 2.0.0) libsoxr0 (2 0.1.1) libstdc++6 (2 6) libsuil-0-0 (2 0.8.0~dfsg0) libtwolame0 (2 0.3.6) libvamp-hostsdk3v5 (2 2.10.0) libvorbis0a (2 1.3.3) libvorbisenc2 (2 1.3.3) libvorbisfile3 (2 1.3.3) libwxbase3.0-0v5 (2 3.0.5.1+dfsg) libwxgtk3.0-gtk3-0v5 (2 3.0.5.1+dfsg) ladspa-plugin (0 (null))
Provides:
2.4.2~dfsg0-5 -
Reverse Provides:
```
__2. Simulate the Installation:__
```sh
sudo apt-get install -s audacity

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
audacity is already the newest version (2.4.2~dfsg0-5).
0 upgraded, 0 newly installed, 0 to remove and 63 not upgraded.

```

## Task 3: Hold and Unhold Package Versions

__1. Install a Package:__
```sh
sudo apt install audacity

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  adwaita-icon-theme alsa-topology-conf alsa-ucm-conf at-spi2-core audacity-data dconf-gsettings-backend
  dconf-service fontconfig gsettings-desktop-schemas gtk-update-icon-cache hicolor-icon-theme humanity-icon-theme
  i965-va-driver intel-media-va-driver libaacs0 libaom3 libasound2 libasound2-data libatk-bridge2.0-0 libatk1.0-0
  libatk1.0-data libatspi2.0-0 libavahi-client3 libavahi-common-data libavahi-common3 libavcodec58 libavformat58
  libavutil56 libbdplus0 libbluray2 libcairo-gobject2 libcairo2 libchromaprint1 libcodec2-1.0 libcolord2 libcups2
  libdatrie1 libdav1d5 libdconf1 libdouble-conversion3 libdrm-amdgpu1 libdrm-intel1 libdrm-nouveau2
  libdrm-radeon1 libegl-mesa0 libegl1 libepoxy0 libflac++6v5 libflac8 libfribidi0 libgail-common libgail18
  libgbm1 libgdk-pixbuf-2.0-0 libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgl1 libgl1-amber-dri
  libgl1-mesa-dri libglapi-mesa libglvnd0 libglx-mesa0 libglx0 libgme0 libgraphite2-3 libgsm1 libgtk-3-0
  libgtk-3-bin libgtk-3-common libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libharfbuzz0b libice6 libid3tag0
  libigdgmm12 libinput-bin libinput10 libjack-jackd2-0 liblcms2-2 liblilv-0-0 libllvm15 libmad0 libmd4c0 libmfx1
  libmp3lame0 libmpg123-0 libmtdev1 libnorm1 libnotify4 libnuma1 libogg0 libopenjp2-7 libopenmpt0 libopus0
  libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpciaccess0 libpcre2-16-0 libpgm-5.3-0 libpixman-1-0
  libportaudio2 libportsmf0v5 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5svg5 libqt5widgets5
  libqt5x11extras5 librabbitmq4 librsvg2-2 librsvg2-common libsamplerate0 libsensors-config libsensors5
  libserd-0-0 libshine3 libsm6 libsnappy1v5 libsndfile1 libsodium23 libsord-0-0 libsoundtouch1 libsoxr0 libspeex1
  libsratom-0-0 libsrt1.4-gnutls libssh-gcrypt-4 libsuil-0-0 libswresample3 libthai-data libthai0 libtheora0
  libtwolame0 libudfread0 libva-drm2 libva-x11-2 libva2 libvamp-hostsdk3v5 libvdpau1 libvorbis0a libvorbisenc2
  libvorbisfile3 libvpx7 libwacom-bin libwacom-common libwacom9 libwayland-client0 libwayland-cursor0
  libwayland-egl1 libwayland-server0 libwebpmux3 libwxbase3.0-0v5 libwxgtk3.0-gtk3-0v5 libx11-xcb1 libx264-163
  libx265-199 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-present0
  libxcb-randr0 libxcb-render-util0 libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-util1
  libxcb-xfixes0 libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxcomposite1 libxcursor1 libxdamage1 libxfixes3
  libxi6 libxinerama1 libxkbcommon-x11-0 libxkbcommon0 libxrandr2 libxrender1 libxshmfence1 libxtst6 libxvidcore4
  libxxf86vm1 libzmq5 libzvbi-common libzvbi0 mesa-va-drivers mesa-vdpau-drivers ocl-icd-libopencl1
  qt5-gtk-platformtheme qttranslations5-l10n session-migration ubuntu-mono va-driver-all vdpau-driver-all
  x11-common
  ...
```
__2. Hold the Package:__
```sh
sudo apt-mark hold audacity

audacity set on hold.
```
__3. Verify the Hold Status:__
```sh
apt-mark showhold

audacity
```
__4. Unhold the Package:__
```sh
sudo apt-mark unhold audacity

Canceled hold on audacity.

apt-mark showhold
nothing
```