# Task 1
## 1. I created a local repository and placed there gnome calculator package

user@user-VirtualBox:~$ mkdir -p ~/local-apt-repo
user@user-VirtualBox:~$ cp ~/Downloads/gnome-calculator_41.1-2ubuntu2_arm64.deb ~/local-apt-repo/
user@user-VirtualBox:~$ cd local-apt-repo/
user@user-VirtualBox:~/local-apt-repo$ ls
gnome-calculator_41.1-2ubuntu2_arm64.deb

## 2. I used dpkg-scanpackages to create a Packages file and compressed it into a Packages.gz archive . From the Packages file I got metadata of my gnome calculator package.

user@user-VirtualBox:~/local-apt-repo$ dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   gnome-calculator
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
user@user-VirtualBox:~/local-apt-repo$ ls
gnome-calculator_41.1-2ubuntu2_arm64.deb  Packages.gz

user@user-VirtualBox:~/local-apt-repo$ cat Packages
Package: gnome-calculator
Version: 1:41.1-2ubuntu2
Architecture: arm64
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Installed-Size: 3464
Depends: libatk1.0-0 (>= 1.12.4), libc6 (>= 2.34), libgee-0.8-2 (>= 0.20), libglib2.0-0 (>= 2.43.92), libgtk-3-0 (>= 3.24.1), libgtksourceview-4-0 (>= 2.91.4), libhandy-1-0 (>= 1.5.90), libmpc3 (>= 1.1.0), libmpfr6 (>= 3.1.3), libsoup2.4-1 (>= 2.42), libxml2 (>= 2.7.4), dconf-gsettings-backend | gsettings-backend
Recommends: yelp, gvfs
Breaks: gcalctool (<< 6.7)
Replaces: gcalctool (<< 6.7)
Filename: /home/user/local-apt-repo/gnome-calculator_41.1-2ubuntu2_arm64.deb
Size: 433676
MD5sum: 05f97d8662fb0a01063855f88d76b620
SHA1: 175ed3491492efd486b6a58e3af314f53ea4cf9c
SHA256: 9c171b4ff3cc1b8c94f320a82df289e720d576d066d2a48bce19c4e3aa930cae
Section: math
Priority: optional
Homepage: https://wiki.gnome.org/Apps/Calculator
Description: GNOME desktop calculator
 The GNOME calculator is a powerful graphical calculator with financial,
 logical and scientific modes. It uses a multiple precision package to do its
 arithmetic to give a high degree of accuracy.
Original-Maintainer: Debian GNOME Maintainers <pkg-gnome-maintainers@lists.alioth.debian.org>

## 3. I added the repository to my sources.list and requested updates

user@user-VirtualBox:~/local-apt-repo$ echo "deb [trusted=yes] file:/home/user/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
deb [trusted=yes] file:/home/user/local-apt-repo ./
user@user-VirtualBox:~/local-apt-repo$ cat /etc/apt/sources.list.d/local-apt-repo.list
deb [trusted=yes] file:/home/user/local-apt-repo ./

user@user-VirtualBox:~/local-apt-repo$ sudo apt update
Get:1 file:/home/user/local-apt-repo ./ InRelease
Ign:1 file:/home/user/local-apt-repo ./ InRelease
Get:2 file:/home/user/local-apt-repo ./ Release
Ign:2 file:/home/user/local-apt-repo ./ Release
Get:3 file:/home/user/local-apt-repo ./ Packages
Ign:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Get:3 file:/home/user/local-apt-repo ./ Packages
Ign:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Get:3 file:/home/user/local-apt-repo ./ Packages
Ign:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Get:3 file:/home/user/local-apt-repo ./ Packages [737 B]
Hit:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Get:3 file:/home/user/local-apt-repo ./ Packages
Ign:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Get:3 file:/home/user/local-apt-repo ./ Packages
Ign:3 file:/home/user/local-apt-repo ./ Packages
Get:4 file:/home/user/local-apt-repo ./ Translation-en
Ign:4 file:/home/user/local-apt-repo ./ Translation-en
Get:5 file:/home/user/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/user/local-apt-repo ./ Translation-en_US
Get:3 file:/home/user/local-apt-repo ./ Packages [1,220 B]
Hit:6 http://ru.archive.ubuntu.com/ubuntu noble InRelease
Hit:7 http://ru.archive.ubuntu.com/ubuntu noble-updates InRelease
Hit:8 http://ru.archive.ubuntu.com/ubuntu noble-backports InRelease
Hit:9 http://security.ubuntu.com/ubuntu noble-security InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
40 packages can be upgraded. Run 'apt list --upgradable' to see them.
N: Download is performed unsandboxed as root as file '/home/user/local-apt-repo/./InRelease' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)

## 4. I Double checked that the Packages.gz file contains the correct paths and metadata:

user@user-VirtualBox:~/local-apt-repo$ zcat Packages.gz
Package: gnome-calculator
Version: 1:41.1-2ubuntu2
Architecture: arm64
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Installed-Size: 3464
Depends: libatk1.0-0 (>= 1.12.4), libc6 (>= 2.34), libgee-0.8-2 (>= 0.20), libglib2.0-0 (>= 2.43.92), libgtk-3-0 (>= 3.24.1), libgtksourceview-4-0 (>= 2.91.4), libhandy-1-0 (>= 1.5.90), libmpc3 (>= 1.1.0), libmpfr6 (>= 3.1.3), libsoup2.4-1 (>= 2.42), libxml2 (>= 2.7.4), dconf-gsettings-backend | gsettings-backend
Recommends: yelp, gvfs
Breaks: gcalctool (<< 6.7)
Replaces: gcalctool (<< 6.7)
Filename: /home/user/local-apt-repo/gnome-calculator_41.1-2ubuntu2_arm64.deb
Size: 433676
MD5sum: 05f97d8662fb0a01063855f88d76b620
SHA1: 175ed3491492efd486b6a58e3af314f53ea4cf9c
SHA256: 9c171b4ff3cc1b8c94f320a82df289e720d576d066d2a48bce19c4e3aa930cae
Section: math
Priority: optional
Homepage: https://wiki.gnome.org/Apps/Calculator
Description: GNOME desktop calculator
 The GNOME calculator is a powerful graphical calculator with financial,
 logical and scientific modes. It uses a multiple precision package to do its
 arithmetic to give a high degree of accuracy.
Original-Maintainer: Debian GNOME Maintainers <pkg-gnome-maintainers@lists.alioth.debian.org>

user@user-VirtualBox:~/local-apt-repo$ apt policy gnome-calculator
gnome-calculator:
  Installed: 1:46.0-1ubuntu1
  Candidate: 1:46.0-1ubuntu1
  Version table:
 *** 1:46.0-1ubuntu1 500
        500 http://ru.archive.ubuntu.com/ubuntu noble/main amd64 Packages
        100 /var/lib/dpkg/status

## 5. I Installed the gnome calculator package

user@user-VirtualBox:~/local-apt-repo$ sudo apt install gnome-calculator
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  gnome-calculator
0 upgraded, 1 newly installed, 0 to remove and 40 not upgraded.
Need to get 435 kB of archives.
After this operation, 3,383 kB of additional disk space will be used.
Get:1 http://ru.archive.ubuntu.com/ubuntu noble/main amd64 gnome-calculator amd64 1:46.0-1ubuntu1 [435 kB]
Fetched 435 kB in 0s (1,303 kB/s)
Selecting previously unselected package gnome-calculator.
(Reading database ... 149839 files and directories currentl
y installed.)
Preparing to unpack .../gnome-calculator_1%3a46.0-1ubuntu1_
amd64.deb ...
Unpacking gnome-calculator (1:46.0-1ubuntu1) ...
Setting up gnome-calculator (1:46.0-1ubuntu1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1.1ubuntu3) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for libglib2.0-0t64:amd64 (2.80.0-6ubun
tu3.1) ...
Processing triggers for desktop-file-utils (0.27-2build1) .
..

# Task 2

## I simulated a gnome-calculator package installation using commands:

User@user-VirtualBox:~$ apt-cache showpkg gnome-calculator
user@user-VirtualBox:~$ sudo apt-get install -s gnome-calculator

## The 1st command showed the dependencies that would be installed:

1:46.0-1ubuntu1 - libadwaita-1-0 (2 1.4~beta) libc6 (2 2.34) libglib2.0-0t64 (2 2.64.0) libgtk-4-1 (2 4.11.4) libgtksourceview-5-0 (2 5.3.0) libmpc3 (2 1.1.0) libmpfr6 (2 3.1.3) libsoup-3.0-0 (2 3.4.0) libxml2 (2 2.7.4) dconf-gsettings-backend (16 (null)) gsettings-backend (0 (null)) gcalctool (3 6.7) yelp (0 (null)) gvfs (0 (null)) gcalctool (3 6.7)

## The 2nd command showed the packages that would be installed:

Inst gnome-calculator (1:46.0-1ubuntu1 Ubuntu:24.04/noble [amd64])
Conf gnome-calculator (1:46.0-1ubuntu1 Ubuntu:24.04/noble [amd64])

# Task 3

## 1. I installed the gnome-calculator package to test holding and unholding options.

user@user-VirtualBox:~$ sudo apt install gnome-calculator
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  gnome-calculator
0 upgraded, 1 newly installed, 0 to remove and 51 not upgraded.
Need to get 435 kB of archives.
After this operation, 3,383 kB of additional disk space will be used.
Get:1 http://ru.archive.ubuntu.com/ubuntu noble/main amd64 gnome-calculator amd64 1:46.0-1ubuntu1 [435 kB]
Fetched 435 kB in 0s (1,143 kB/s)
Selecting previously unselected package gnome-calculator.
(Reading database ... 149839 files and directories currentl
y installed.)
Preparing to unpack .../gnome-calculator_1%3a46.0-1ubuntu1_
amd64.deb ...
Unpacking gnome-calculator (1:46.0-1ubuntu1) ...
Setting up gnome-calculator (1:46.0-1ubuntu1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1.1ubuntu3) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for libglib2.0-0t64:amd64 (2.80.0-6ubun
tu3.1) ...
Processing triggers for desktop-file-utils (0.27-2build1) .
..

## 2. I marked the package as held. Then I verified that the package was indeed held, using showhold option.

user@user-VirtualBox:~$ sudo apt-mark hold gnome-calculator
gnome-calculator set on hold.
user@user-VirtualBox:~$ apt-mark showhold
gnome-calculator

## 3. Then I marked the package as unheld and verified that  it was no longer on the hold list.

user@user-VirtualBox:~$ sudo apt-mark unhold gnome-calculator
Canceled hold on gnome-calculator.
user@user-VirtualBox:~$ apt-mark showhold
