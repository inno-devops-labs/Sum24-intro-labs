# Lab 4. Software Distribution

## Task 1. Configure and Use a Local Package Repository

1. Create folder for repository and copy .deb file to it

```
root@dimoninbirsk:~# mkdir -p ~/local-apt-repo
root@dimoninbirsk:~# cp /root/fonts-gargi_2.0-5_all.deb  ~/local-apt-repo/
```

2. Generate the Packages.gz file

```
root@dimoninbirsk:~# dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   fonts-gargi_2.0-5_all.deb
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
```

3. Add repository to repository list in ``/etc/apt/sources.list``

```
root@dimoninbirsk:~# echo "deb [trusted=yes] file:/root/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
sudo apt update

Get:1 file:/root/local-apt-repo ./ InRelease
Ign:1 file:/root/local-apt-repo ./ InRelease
Get:3 file:/root/local-apt-repo ./ Release
Ign:3 file:/root/local-apt-repo ./ Release
Get:5 file:/root/local-apt-repo ./ Packages
Ign:5 file:/root/local-apt-repo ./ Packages
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Get:5 file:/root/local-apt-repo ./ Packages
Ign:5 file:/root/local-apt-repo ./ Packages
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Get:5 file:/root/local-apt-repo ./ Packages
Ign:5 file:/root/local-apt-repo ./ Packages
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Get:5 file:/root/local-apt-repo ./ Packages [530 B]
Ign:5 file:/root/local-apt-repo ./ Packages
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Get:5 file:/root/local-apt-repo ./ Packages
Ign:5 file:/root/local-apt-repo ./ Packages
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Get:5 file:/root/local-apt-repo ./ Packages
Ign:5 file:/root/local-apt-repo ./ Packages
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Get:5 file:/root/local-apt-repo ./ Packages
Err:5 file:/root/local-apt-repo ./ Packages
  File not found - /root/local-apt-repo/./Packages (2: No such file or directory)
Get:6 file:/root/local-apt-repo ./ Translation-en
Ign:6 file:/root/local-apt-repo ./ Translation-en
Reading package lists... Done
```

4. Check content of package

```
root@dimoninbirsk:~/local-apt-repo# zcat Packages.gz
Package: fonts-gargi
Version: 2.0-5
Architecture: all
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Installed-Size: 91
Enhances: fonts-deva-extra
Filename: /root/local-apt-repo/fonts-gargi_2.0-5_all.deb
Size: 42364
MD5sum: 1bb8e0eabf76f8054bb70415e97d81cc
SHA1: aa64a3a245468b415ec90a003b8ccc23075cafcc
SHA256: 347746cabe316a2c29520072df8088cc26de91565b23068898fe4f5e26a1f0de
Section: fonts
Priority: optional
Multi-Arch: foreign
Description: OpenType Devanagari font
 This package provides Gargi font for Devanagari script which is
 used as script for multiple languages such as Hindi, Kashmiri,
 Konkani, Maithili, Marathi normally spoken in various states
 in Indian subcontinent.
Original-Maintainer: Debian Fonts Task Force <debian-fonts@lists.debian.org>

root@dimoninbirsk:~/local-apt-repo# apt policy fonts-gargi
fonts-gargi:
  Installed: (none)
  Candidate: 2.0-5
  Version table:
     2.0-5 500
        500 http://mirror.hoztnode.net/ubuntu jammy/main amd64 Packages
```

5. Install package

```
root@dimoninbirsk:~/local-apt-repo# sudo apt install fonts-gargi
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  fonts-gargi
0 upgraded, 1 newly installed, 0 to remove and 63 not upgraded.
Need to get 42.4 kB of archives.
After this operation, 93.2 kB of additional disk space will be used.
Get:1 file:/root/local-apt-repo ./ fonts-gargi all 2.0-5 [42.4 kB]
Selecting previously unselected package fonts-gargi.
(Reading database ... 107478 files and directories currently installed.)
Preparing to unpack .../fonts-gargi_2.0-5_all.deb ...
Unpacking fonts-gargi (2.0-5) ...
Setting up fonts-gargi (2.0-5) ...

----------------------
```

## Task 2. Simulate Package Installation and Identify Dependencies

1. Use previous font package

```
root@dimoninbirsk:~/local-apt-repo# apt-cache showpkg fonts-gargi
Package: fonts-gargi
Versions:
2.0-5 (/var/lib/apt/lists/_root_local-apt-repo_Packages) (/var/lib/dpkg/status)
Description Language:
File: /var/lib/apt/lists/_root_local-apt-repo_Packages
MD5: 55972338623ca2cee6e07708a9d6ae30


Reverse Depends:
  fonts-deva,fonts-gargi
  marsshooter,fonts-gargi
  fonts-sarai,fonts-gargi
  fonts-deva-extra,fonts-gargi
Dependencies:
2.0-5 - fonts-deva-extra (0 (null))
Provides:
2.0-5 -
Reverse Provides:
```

2. Simulate the Installation:

```
root@dimoninbirsk:~/local-apt-repo# sudo apt-get install -s fonts-gargi
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
fonts-gargi is already the newest version (2.0-5).
0 upgraded, 0 newly installed, 0 to remove and 63 not upgraded.
```

3. Due that this package is a font package, there is nott a lot of dependencies. Only one: ``fonts-deva-extra (0 (null))``.

## Task 3. Hold and Unhold Package Versions

1. Update ``nano`` redactor

```
root@dimoninbirsk:~/local-apt-repo# sudo apt install nano
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
nano is already the newest version (6.2-1).
0 upgraded, 0 newly installed, 0 to remove and 63 not upgraded.
```

2. Prevent ``nano`` from updating

```
root@dimoninbirsk:~/local-apt-repo# sudo apt-mark hold nano
nano set on hold.
```

3. Check, is nano prevented from update

```
root@dimoninbirsk:~/local-apt-repo# apt-mark showhold
nano
```

4. Return to normal state

```
root@dimoninbirsk:~/local-apt-repo# sudo apt-mark unhold nano
Canceled hold on nano.
root@dimoninbirsk:~/local-apt-repo# apt-mark showhold
root@dimoninbirsk:~/local-apt-repo#
```
