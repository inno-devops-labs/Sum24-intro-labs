# Lab 4: Software Distribution
## Anton Buguev, a.buguev@innopolis.university, M23-RO-01

### Task 1. Configure and Use a Local Package Repository

1. Create folder and copy `.deb` file in it:
```sh
$ mkdir -p ~/local-apt-repo
$ cp Downloads/google-chrome-stable_current_amd64.deb ~/local-apt-repo/
```

2. Create a Packages file
```sh
$ dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz

dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   google-chrome-stable
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
```

3. Add the repository to `sources.list`:
```sh
$ echo "deb [trusted=yes] file:/home/anton/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list 

deb [trusted=yes] file:/home/anton/local-apt-repo ./
```

4. Verify the Contents of the Packages.gz File:
```sh
$ zcat local-apt-repo/Packages.gz

Package: google-chrome-stable
Version: 126.0.6478.126-1
Architecture: amd64
Maintainer: Chrome Linux Team <chromium-dev@chromium.org>
Installed-Size: 340311
Pre-Depends: dpkg (>= 1.14.0)
Depends: ca-certificates, fonts-liberation, libasound2 (>= 1.0.17), libatk-bridge2.0-0 (>= 2.5.3), libatk1.0-0 (>= 2.2.0), libatspi2.0-0 (>= 2.9.90), libc6 (>= 2.17), libcairo2 (>= 1.6.0), libcups2 (>= 1.6.0), libcurl3-gnutls | libcurl3-nss | libcurl4 | libcurl3, libdbus-1-3 (>= 1.9.14), libdrm2 (>= 2.4.75), libexpat1 (>= 2.1~beta3), libgbm1 (>= 17.1.0~rc2), libglib2.0-0 (>= 2.39.4), libgtk-3-0 (>= 3.9.10) | libgtk-4-1, libnspr4 (>= 2:4.9-2~), libnss3 (>= 2:3.35), libpango-1.0-0 (>= 1.14.0), libu2f-udev, libvulkan1, libx11-6 (>= 2:1.4.99.1), libxcb1 (>= 1.9.2), libxcomposite1 (>= 1:0.4.4-1), libxdamage1 (>= 1:1.1), libxext6, libxfixes3, libxkbcommon0 (>= 0.5.0), libxrandr2, wget, xdg-utils (>= 1.0.2)
Provides: www-browser
Filename: /home/anton/local-apt-repo/google-chrome-stable_current_amd64.deb
Size: 108773084
MD5sum: d56770acc540af16f377316646dd774a
SHA1: 1d22a19710426f41884f6d2a41415bd70824ff7a
SHA256: 3ec1cadbb55cf66cc51f0421eace324a88836ee2d982b945b8f67a3f131b0924
Section: web
Priority: optional
Description: The web browser from Google
 Google Chrome is a browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

```

```sh
$ apt policy google-chrome-stable

google-chrome-stable:
  Installed: 125.0.6422.141-1
  Candidate: 126.0.6478.126-1
  Version table:
     126.0.6478.126-1 500
        500 https://dl.google.com/linux/chrome/deb stable/main amd64 Packages
        500 file:/home/anton/local-apt-repo ./ Packages
 *** 125.0.6422.141-1 100
        100 /var/lib/dpkg/status
```

5. Install file from local repository
```sh
$ sudo apt install google-chrome-stable

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  python3-cliapp python3-markdown python3-packaging python3-ttystatus
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  google-chrome-stable
0 upgraded, 1 newly installed, 0 to remove and 48 not upgraded.
Need to get 109 MB of archives.
After this operation, 348 MB of additional disk space will be used.
Get:1 https://dl.google.com/linux/chrome/deb stable/main amd64 google-chrome-stable amd64 126.0.6478.126-1 [109 MB]
Fetched 109 MB in 11s (9 975 kB/s)                                             
Selecting previously unselected package google-chrome-stable.
(Reading database ... 374917 files and directories currently installed.)
Preparing to unpack .../google-chrome-stable_126.0.6478.126-1_amd64.deb ...
Unpacking google-chrome-stable (126.0.6478.126-1) ...
Setting up google-chrome-stable (126.0.6478.126-1) ...
update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/x-w
ww-browser (x-www-browser) in auto mode
update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/gno
me-www-browser (gnome-www-browser) in auto mode
update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/goo
gle-chrome (google-chrome) in auto mode
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu3) ...
```

### Task 2. Simulate Package Installation and Identify Dependencies.

1. Check package info
```sh
$ apt-cache showpkg google-chrome-stable 

Package: google-chrome-stable
Versions: 
126.0.6478.126-1 (/var/lib/apt/lists/dl.google.com_linux_chrome_deb_dists_stable_main_binary-amd64_Packages) (/var/lib/apt/lists/_home_anton_local-apt-repo_._Packages) (/var/lib/dpkg/status)
 Description Language: 
                 File: /var/lib/apt/lists/dl.google.com_linux_chrome_deb_dists_stable_main_binary-amd64_Packages
                  MD5: a2d34067fc33f1c87253c33b9fd975f0


Reverse Depends: 
Dependencies: 
126.0.6478.126-1 - dpkg (2 1.14.0) ca-certificates (0 (null)) fonts-liberation (0 (null)) libasound2 (2 1.0.17) libatk-bridge2.0-0 (2 2.5.3) libatk1.0-0 (2 2.2.0) libatspi2.0-0 (2 2.9.90) libc6 (2 2.17) libcairo2 (2 1.6.0) libcups2 (2 1.6.0) libcurl3-gnutls (16 (null)) libcurl3-nss (16 (null)) libcurl4 (16 (null)) libcurl3 (0 (null)) libdbus-1-3 (2 1.9.14) libdrm2 (2 2.4.75) libexpat1 (2 2.1~beta3) libgbm1 (2 17.1.0~rc2) libglib2.0-0 (2 2.39.4) libgtk-3-0 (18 3.9.10) libgtk-4-1 (0 (null)) libnspr4 (2 2:4.9-2~) libnss3 (2 2:3.35) libpango-1.0-0 (2 1.14.0) libu2f-udev (0 (null)) libvulkan1 (0 (null)) libx11-6 (2 2:1.4.99.1) libxcb1 (2 1.9.2) libxcomposite1 (2 1:0.4.4-1) libxdamage1 (2 1:1.1) libxext6 (0 (null)) libxfixes3 (0 (null)) libxkbcommon0 (2 0.5.0) libxrandr2 (0 (null)) wget (0 (null)) xdg-utils (2 1.0.2) 
Provides: 
126.0.6478.126-1 - www-browser (= ) 
Reverse Provides: 
```
Here we can see what dependencies the package has and what it provides.

2. Simulate installation
```sh
$ sudo apt install -s google-chrome-stable

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  python3-cliapp python3-markdown python3-packaging python3-ttystatus
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  google-chrome-stable
0 upgraded, 1 newly installed, 0 to remove and 48 not upgraded.
Inst google-chrome-stable (126.0.6478.126-1 Google:1.0/stable, localhost [amd64])
Conf google-chrome-stable (126.0.6478.126-1 Google:1.0/stable, localhost [amd64])
```

Package was not indeed installed:
```sh
$ dpkg -s google-chrome-stable 

Package: google-chrome-stable
Status: deinstall ok config-files
```

### Task 3. Hold and Unhold Package Versions.

1. Install package:
```sh
$ sudo apt install google-chrome-stable

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  python3-cliapp python3-markdown python3-packaging python3-ttystatus
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  google-chrome-stable
0 upgraded, 1 newly installed, 0 to remove and 48 not upgraded.
Need to get 109 MB of archives.
After this operation, 348 MB of additional disk space will be used.
Get:1 https://dl.google.com/linux/chrome/deb stable/main amd64 google-chrome-stable amd64 126.0.6478.126-1 [109 MB]
Fetched 109 MB in 11s (9 975 kB/s)                                             
Selecting previously unselected package google-chrome-stable.
(Reading database ... 374917 files and directories currently installed.)
Preparing to unpack .../google-chrome-stable_126.0.6478.126-1_amd64.deb ...
Unpacking google-chrome-stable (126.0.6478.126-1) ...
Setting up google-chrome-stable (126.0.6478.126-1) ...
update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/x-w
ww-browser (x-www-browser) in auto mode
update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/gno
me-www-browser (gnome-www-browser) in auto mode
update-alternatives: using /usr/bin/google-chrome-stable to provide /usr/bin/goo
gle-chrome (google-chrome) in auto mode
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu3) ...
```

2. Hold the package:
```sh
$ sudo apt-mark hold google-chrome-stable

google-chrome-stable set on hold.
```

3. Verify the Hold Status:
```sh
$ apt-mark showhold

google-chrome-stable
```

4. Unhold the Package:
```sh
$ sudo apt-mark unhold google-chrome-stable

Canceled hold on google-chrome-stable.
```

5. Check Hold Status adter Unhold:
```sh
$ apt-mark showhold
$ <nothing>
```
