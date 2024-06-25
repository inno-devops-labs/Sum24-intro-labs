# Lab 4 : Software Distribution

## Task 1: Configure and Use a Local Package Repository

1. **Creating a Local Repository**:
   - For my pakage i will use Google chrome. I downloaded the `.deb` file and copied it to the `local-apt-repo` directory. 
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ ls
    chrome
    suwilanji@SUWILANJI-PCV3:~$ mkdir -p ~/local-apt-repo
    suwilanji@SUWILANJI-PCV3:~$ cp ~/chrome/google-chrome-stable_current_amd64.deb ~/local-apt-repo/
    suwilanji@SUWILANJI-PCV3:~$ ls
    chrome  local-apt-repo
    ```

2. **Generate the Package Index**:
   - Using `dpkg-scanpackages` creates a `Packages` file and `gzip -9c` compresss this file into a `Packages.gz` archive.

    ```sh
    suwilanji@SUWILANJI-PCV3:~$ dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
    dpkg-scanpackages: warning: Packages in archive but missing from override file:
    dpkg-scanpackages: warning:   google-chrome-stable
    dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
    ```

3. **Add the Local Repository to Your Sources List**:
   - I used the following command to ass the repository to my `sources.list`.
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ echo "deb [trusted=yes] file:/home/suwilanji/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo list
    deb [trusted=yes] file:/home/suwilanji/local-apt-repo ./
    ```
    - Before uupdating the reposory I changed the filename genrated in the Pakages.gz to in the following format 
    ```sh
    Filename: ./google-chrome-stable_current_amd64.deb
    ```
    - And i updaded the apt repository by running 
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt update
    Get:1 file:/home/suwilanji/local-apt-repo ./ InRelease
    Ign:1 file:/home/suwilanji/local-apt-repo ./ InRelease
    Get:2 file:/home/suwilanji/local-apt-repo ./ Release
    Ign:2 file:/home/suwilanji/local-apt-repo ./ Release
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Ign:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Ign:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Ign:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Ign:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Ign:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Ign:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages [772 B]
    Hit:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Err:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    File not found - /home/suwilanji/local-apt-repo/./en.gz (2: No such file or directory)
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Err:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    File not found - /home/suwilanji/local-apt-repo/./en.lz4 (2: No such file or directory)
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Err:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    File not found - /home/suwilanji/local-apt-repo/./en.zst (2: No such file or directory)
    Get:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Ign:4 file:/home/suwilanji/local-apt-repo ./ Translation-en
    Err:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Could not open file /home/suwilanji/local-apt-repo/./Packages - open (13: Permission denied)
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Err:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Method gave a blank filename
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Err:3 file:/home/suwilanji/local-apt-repo ./ Packages
    Method gave a blank filename
    Get:3 file:/home/suwilanji/local-apt-repo ./ Packages [1353 B]
    Get:5 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
    Get:6 https://dl.google.com/linux/chrome/deb stable InRelease [1825 B]
    Get:7 https://dl.google.com/linux/chrome/deb stable/main amd64 Packages [1087 B]
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    2 packages can be upgraded. Run 'apt list --upgradable' to see them.
    ```

4. **Verify the Contents of the Packages.gz File:**:
   - To verify the contents of my .deb file I used the following command. 

    ```sh
    suwilanji@SUWILANJI-PCV3:~/local-apt-repo$ zcat Packages.gz
    Package: google-chrome-stable
    Version: 126.0.6478.126-1
    Architecture: amd64
    Maintainer: Chrome Linux Team <chromium-dev@chromium.org>
    Installed-Size: 340311
    Pre-Depends: dpkg (>= 1.14.0)
    Depends: ca-certificates, fonts-liberation, libasound2 (>= 1.0.17), libatk-bridge2.0-0 (>= 2.5.3), libatk1.0-0 (>= 2.2.0), libatspi2.0-0 (>= 2.9.90), libc6 (>= 2.17), libcairo2 (>= 1.6.0), libcups2 (>= 1.6.0), libcurl3-gnutls | libcurl3-nss | libcurl4 | libcurl3, libdbus-1-3 (>= 1.9.14), libdrm2 (>= 2.4.75), libexpat1 (>= 2.1~beta3), libgbm1 (>= 17.1.0~rc2), libglib2.0-0 (>= 2.39.4), libgtk-3-0 (>= 3.9.10) | libgtk-4-1, libnspr4 (>= 2:4.9-2~), libnss3 (>= 2:3.35), libpango-1.0-0 (>= 1.14.0), libu2f-udev, libvulkan1, libx11-6 (>= 2:1.4.99.1), libxcb1 (>= 1.9.2), libxcomposite1 (>= 1:0.4.4-1), libxdamage1 (>= 1:1.1), libxext6, libxfixes3, libxkbcommon0 (>= 0.5.0), libxrandr2, wget, xdg-utils (>= 1.0.2)
    Provides: www-browser
    Filename: ./google-chrome-stable_current_amd64.deb
    Size: 108773084
    Installed: (none)
    Candidate: 126.0.6478.126-1
    Version table:
        126.0.6478.126-1 500
            500 https://dl.google.com/linux/chrome/deb stable/main amd64 Packages
            500 file:/home/suwilanji/local-apt-repo ./ Packages
            100 /var/lib/dpkg/status
    ```
    - Since I already had one chrome pakage from google chrome, i removed it first before installing the pakage from my local-apt-repo
    ```sh
    suwilanji@SUWILANJI-PCV3:~/local-apt-repo$ sudo rm /etc/apt/sources.list.d/
    google-chrome.list   local-apt-repo.list
    suwilanji@SUWILANJI-PCV3:~/local-apt-repo$ sudo rm /etc/apt/sources.list.d/google-chrome.list
    ```
    - My chrome pakage apt policy
    ```sh
    suwilanji@SUWILANJI-PCV3:~/local-apt-repo$ apt policy google-chrome-stable
    google-chrome-stable:
    Installed: (none)
    Candidate: 126.0.6478.126-1
    Version table:
        126.0.6478.126-1 500
            500 file:/home/suwilanji/local-apt-repo ./ Packages
            100 /var/lib/dpkg/status
    ```

5. **Install a Package from the Local Repository**:
   - Installing my pakage from my local repository gives the following result

    ```sh
    suwilanji@SUWILANJI-PCV3:~/local-apt-repo$ sudo apt install google-chrome-stable
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    The following NEW packages will be installed:
    google-chrome-stable
    0 upgraded, 1 newly installed, 0 to remove and 2 not upgraded.
    Need to get 0 B/109 MB of archives.
    After this operation, 348 MB of additional disk space will be used.
    Get:1 file:/home/suwilanji/local-apt-repo ./ google-chrome-stable 126.0.6478.126-1 [109 MB]
    Selecting previously unselected package google-chrome-stable.
    (Reading database ... 46342 files and directories currently installed.)
    Preparing to unpack .../google-chrome-stable_current_amd64.deb ...
    Unpacking google-chrome-stable (126.0.6478.126-1) ...
    Setting up google-chrome-stable (126.0.6478.126-1) ...
    update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/x-www-browser (x-www-browser) in auto mode
    update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/gnome-www-browser (gnome-www-browser) in auto mode
    update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/google-chrome (google-chrome) in auto mode
    Processing triggers for man-db (2.10.2-1) ...
    suwilanji@SUWILANJI-PCV3:~/local-apt-repo$ google-chrome-stable --version
    Google Chrome 126.0.6478.126
    ```
## Task 2: Simulate Package Installation and Identify Dependencies

1. **Choose a Package to Simulate**:
   - For the installation simulation i will use google chrome again, so before i start i will first remove google-chrome-stable
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt remove google-chrome-stable
    [sudo] password for suwilanji:
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    The following packages were automatically installed and are no longer required:
    adwaita-icon-theme alsa-topology-conf alsa-ucm-conf at-spi2-core dconf-gsettings-backend dconf-service fontconfig
    libencode-locale-perl libepoxy0 libfile-basedir-perl libfile-desktopentry-perl libfile-listing-perl
    libfile-mimeinfo-perl libfont-afm-perl libfontenc1 libgbm1 libgdk-pixbuf-2.0-0 libgdk-pixbuf2.0-bin
    libgdk-pixbuf2.0-common libgl1 libgl1-amber-dri libgl1-mesa-dri libglapi-mesa libglvnd0 libglx-mesa0 libglx0
    libgraphite2-3 libgtk-3-0 libgtk-3-bin libgtk-3-common libgtkd-3-0 libharfbuzz0b libhtml-form-perl
    libhtml-format-perl libhtml-parser-perl libhtml-tagset-perl libhtml-tree-perl libhttp-cookies-perl
    libhttp-daemon-perl libhttp-date-perl libhttp-message-perl libhttp-negotiate-perl libice6 libio-html-perl
    libio-socket-ssl-perl libio-stringy-perl libipc-system-simple-perl liblcms2-2 libllvm11 libllvm15
    liblwp-mediatypes-perl liblwp-protocol-https-perl libmailtools-perl libnet-dbus-perl libnet-http-perl
    libnet-smtp-ssl-perl libnet-ssleay-perl libnspr4 libnss3 libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0
    libpciaccess0 libphobos2-ldc-shared98 libpixman-1-0 librsvg2-2 librsvg2-common libsensors-config libsensors5 libsm6
    libthai-data libthai0 libtie-ixhash-perl libtimedate-perl libtry-tiny-perl libu2f-udev liburi-perl libvte-2.91-0
    libvte-2.91-common libvted-3-0 libvulkan1 libwayland-client0 libwayland-cursor0 libwayland-egl1 libwayland-server0
    libwww-perl libwww-robotrules-perl libx11-protocol-perl libx11-xcb1 libxaw7 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0
    libxcb-present0 libxcb-randr0 libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-xfixes0 libxcomposite1
    libxcursor1 libxdamage1 libxfixes3 libxft2 libxi6 libxinerama1 libxkbcommon0 libxkbfile1 libxml-parser-perl
    libxml-twig-perl libxml-xpathengine-perl libxmu6 libxrandr2 libxrender1 libxshmfence1 libxt6 libxtst6 libxv1
    libxxf86dga1 libxxf86vm1 mesa-vulkan-drivers perl-openssl-defaults session-migration tilix tilix-common ubuntu-mono
    x11-common x11-utils x11-xserver-utils xdg-utils
    Use 'sudo apt autoremove' to remove them.
    The following packages will be REMOVED:
    google-chrome-stable
    0 upgraded, 0 newly installed, 1 to remove and 2 not upgraded.
    After this operation, 348 MB disk space will be freed.
    Do you want to continue? [Y/n] Y
    (Reading database ... 46457 files and directories currently installed.)
    Removing google-chrome-stable (126.0.6478.126-1) ...
    Processing triggers for man-db (2.10.2-1) ...
    ```
    - Checking if it has been removed
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ google-chrome-stable --version
    google-chrome-stable: command not found
    ``` 
    - To simulate the installation i used 

    ```sh
    suwilanji@SUWILANJI-PCV3:~$ apt-cache showpkg google-chrome-stable
    Package: google-chrome-stable
    Versions:
    126.0.6478.126-1 (/var/lib/apt/lists/_home_suwilanji_local-apt-repo_._Packages) (/var/lib/dpkg/status)
    Description Language:
                    File: /var/lib/apt/lists/_home_suwilanji_local-apt-repo_._Packages
                    MD5: a2d34067fc33f1c87253c33b9fd975f0
    Reverse Depends:
    Dependencies:
    126.0.6478.126-1 - dpkg (2 1.14.0) ca-certificates (0 (null)) fonts-liberation (0 (null)) libasound2 (2 1.0.17) libatk-bridge2.0-0 (2 2.5.3) libatk1.0-0 (2 2.2.0) libatspi2.0-0 (2 2.9.90) libc6 (2 2.17) libcairo2 (2 1.6.0) libcups2 (2 1.6.0) libcurl3-gnutls (16 (null)) libcurl3-nss (16 (null)) libcurl4 (16 (null)) libcurl3 (0 (null)) libdbus-1-3 (2 1.9.14) libdrm2 (2 2.4.75) libexpat1 (2 2.1~beta3) libgbm1 (2 17.1.0~rc2) libglib2.0-0 (2 2.39.4) libgtk-3-0 (18 3.9.10) libgtk-4-1 (0 (null)) libnspr4 (2 2:4.9-2~) libnss3 (2 2:3.35) libpango-1.0-0 (2 1.14.0) libu2f-udev (0 (null)) libvulkan1 (0 (null)) libx11-6 (2 2:1.4.99.1) libxcb1 (2 1.9.2) libxcomposite1 (2 1:0.4.4-1) libxdamage1 (2 1:1.1) libxext6 (0 (null)) libxfixes3 (0 (null)) libxkbcommon0 (2 0.5.0) libxrandr2 (0 (null)) wget (0 (null)) xdg-utils (2 1.0.2)
    Provides:
    126.0.6478.126-1 - www-browser (= )
    Reverse Provides:
    suwilanji@SUWILANJI-PCV3:~$
    ```
     - Here we can see many dependencies that the package needs ``` 126.0.6478.126-1 - dpkg (2 1.14.0) ca-certificates (0 (null)) fonts-liberation and many more ```


2. **Simulate the Installation**:
    - I simulate the installation using the ```apt-get install``` command with the ```-s``` flag.
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt-get install -s google-chrome-stable
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    The following NEW packages will be installed:
    google-chrome-stable
    0 upgraded, 1 newly installed, 0 to remove and 2 not upgraded.
    Inst google-chrome-stable (126.0.6478.126-1 localhost [amd64])
    Conf google-chrome-stable (126.0.6478.126-1 localhost [amd64])
    suwilanji@SUWILANJI-PCV3:~$
    ```
    - Upon checking we can see that google chrome has not been actually installed.
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ google-chrome-stable --version
    google-chrome-stable: command not found
    suwilanji@SUWILANJI-PCV3:~$
    ```
## Task 3: Hold and Unhold Package Versions

- I will use the telegram desktop pakage to demonstrate how to hold and unhold a pakage.

1. **Install a Package**:
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt install telegram-desktop
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    The following packages were automatically installed and are no longer required:
    libauthen-sasl-perl libclone-perl libdata-dump-perl libencode-locale-perl libfile-basedir-perl libfile-desktopentry-perl libfile-listing-perl libfile-mimeinfo-perl libfont-afm-perl
    libfontenc1 libgtkd-3-0 libhtml-form-perl libhtml-format-perl libhtml-parser-perl libhtml-tagset-perl libhtml-tree-perl libhttp-cookies-perl libhttp-daemon-perl libhttp-date-perl
    libhttp-message-perl libhttp-negotiate-perl libio-html-perl libio-socket-ssl-perl libio-stringy-perl libipc-system-simple-perl libllvm11 liblwp-mediatypes-perl
    liblwp-protocol-https-perl libmailtools-perl libnet-dbus-perl libnet-http-perl libnet-smtp-ssl-perl libnet-ssleay-perl libnspr4 libnss3 libphobos2-ldc-shared98 libtie-ixhash-perl
    libtimedate-perl libtry-tiny-perl libu2f-udev liburi-perl libvte-2.91-0 libvte-2.91-common libvted-3-0 libvulkan1 libwww-perl libwww-robotrules-perl libx11-protocol-perl libxaw7
    libxft2 libxkbfile1 libxml-parser-perl libxml-twig-perl libxml-xpathengine-perl libxmu6 libxt6 libxv1 libxxf86dga1 mesa-vulkan-drivers perl-openssl-defaults tilix tilix-common
    x11-utils x11-xserver-utils xdg-utils
    Use 'sudo apt autoremove' to remove them.
    The following NEW packages will be installed:
    telegram-desktop
    0 upgraded, 1 newly installed, 0 to remove and 2 not upgraded.
    Need to get 27.9 MB of archives.
    After this operation, 79.2 MB of additional disk space will be used.
    Get:1 http://archive.ubuntu.com/ubuntu jammy/universe amd64 telegram-desktop amd64 3.6.1+ds-2build1 [27.9 MB]
    Fetched 27.9 MB in 3s (10.9 MB/s)
    Selecting previously unselected package telegram-desktop.
    (Reading database ... 48144 files and directories currently installed.)
    Preparing to unpack .../telegram-desktop_3.6.1+ds-2build1_amd64.deb ...
    Unpacking telegram-desktop (3.6.1+ds-2build1) ...
    Setting up telegram-desktop (3.6.1+ds-2build1) ...
    Processing triggers for hicolor-icon-theme (0.17-2) ...
    Processing triggers for man-db (2.10.2-1) ...
    suwilanji@SUWILANJI-PCV3:~$
    ```

2. **Hold the Package**:
    - Using `apt-mark hold` sets the package on hold.
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt-mark hold telegram-desktop
    telegram-desktop set on hold.
    suwilanji@SUWILANJI-PCV3:~$
    ```
3. **Verify the Hold Status**:
    - We can check the hold status of pakages using ```apt-mark showhold```. We can see that telegram-desktop on hold.
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt-mark hold telegram-desktop
    telegram-desktop set on hold.
    suwilanji@SUWILANJI-PCV3:~$ apt-mark showhold
    telegram-desktop
    suwilanji@SUWILANJI-PCV3:~$
    ```

4. **Unhold the Package**:
    - Using `apt-mark unhold` sets the package to unhold and upon checking the hold status we can see that the telegram-desktop pakage is no longer on hold.
    ```sh
    suwilanji@SUWILANJI-PCV3:~$ sudo apt-mark unhold telegram-desktop
    Canceled hold on telegram-desktop.
    suwilanji@SUWILANJI-PCV3:~$ apt-mark showhold
    suwilanji@SUWILANJI-PCV3:~$
    ```
