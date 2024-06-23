# Lab 4: Software Distribution

## Task 1: Configure and Use a Local Package Repository

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ mkdir -p ~/local-apt-repo

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ cp ~/Downloads/zoom_amd64.deb  ~/local-apt-repo/

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ dpkg-scanpackages ~/local-apt-repo /dev/null > ~/local-apt-repo/Packages
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   zoom
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ echo "deb [trusted=yes] file:/home/igor/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
deb [trusted=yes] file:/home/igor/local-apt-repo ./

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ sudo apt update
Get:1 file:/home/igor/local-apt-repo ./ InRelease
Ign:1 file:/home/igor/local-apt-repo ./ InRelease
Get:2 file:/home/igor/local-apt-repo ./ Release
Ign:2 file:/home/igor/local-apt-repo ./ Release
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Get:3 file:/home/igor/local-apt-repo ./ Packages [1 565 B]
Get:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:5 file:/home/igor/local-apt-repo ./ Translation-en
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en
Hit:6 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Get:7 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]                              
Hit:8 http://security.ubuntu.com/ubuntu jammy-security InRelease                                        
Hit:9 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease                                     
Hit:10 https://download.docker.com/linux/ubuntu jammy InRelease                                         
Hit:11 https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/jammy pgadmin4 InRelease                    
Hit:12 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu jammy InRelease    
Hit:13 https://ppa.launchpadcontent.net/obsproject/obs-studio/ubuntu jammy InRelease
Fetched 128 kB in 1s (98,5 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
57 packages can be upgraded. Run 'apt list --upgradable' to see them.
N: Download is performed unsandboxed as root as file '/home/igor/local-apt-repo/./InRelease' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ apt policy zoom
zoom:
  Installed: (none)
  Candidate: 6.1.0.198
  Version table:
     6.1.0.198 500
        500 file:/home/igor/local-apt-repo ./ Packages

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ sudo apt install zoom
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libegl1-mesa libgl1-mesa-glx libxcb-cursor0 libxcb-xtest0
The following NEW packages will be installed:
  libegl1-mesa libgl1-mesa-glx libxcb-cursor0 libxcb-xtest0 zoom
0 upgraded, 5 newly installed, 0 to remove and 57 not upgraded.
Need to get 0 B/205 MB of archives.
After this operation, 711 MB of additional disk space will be used.
Do you want to continue? [Y/n] 
Get:1 file:/home/igor/local-apt-repo ./ zoom 6.1.0.198 [205 MB]
Err:1 file:/home/igor/local-apt-repo ./ zoom 6.1.0.198
  File not found - /home/igor/local-apt-repo//home/igor/local-apt-repo/zoom_amd64.deb (2: No such file or directory)
N: Download is performed unsandboxed as root as file '/home/igor/local-apt-repo//home/igor/local-apt-repo/zoom_amd64.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)
E: Failed to fetch file:/home/igor/local-apt-repo//home/igor/local-apt-repo/zoom_amd64.deb  File not found - /home/igor/local-apt-repo//home/igor/local-apt-repo/zoom_amd64.deb (2: No such file or directory)
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ sudo apt update
Get:1 file:/home/igor/local-apt-repo ./ InRelease
Ign:1 file:/home/igor/local-apt-repo ./ InRelease
Get:2 file:/home/igor/local-apt-repo ./ Release
Ign:2 file:/home/igor/local-apt-repo ./ Release
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:3 file:/home/igor/local-apt-repo ./ Packages
Ign:3 file:/home/igor/local-apt-repo ./ Packages
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Get:3 file:/home/igor/local-apt-repo ./ Packages [1 565 B]
Get:4 file:/home/igor/local-apt-repo ./ Translation-en
Ign:4 file:/home/igor/local-apt-repo ./ Translation-en
Get:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Ign:5 file:/home/igor/local-apt-repo ./ Translation-en_US
Hit:6 http://ru.archive.ubuntu.com/ubuntu jammy InRelease
Get:7 http://ru.archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]                              
Hit:8 https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/jammy pgadmin4 InRelease                      
Hit:9 http://ru.archive.ubuntu.com/ubuntu jammy-backports InRelease                                     
Hit:10 https://download.docker.com/linux/ubuntu jammy InRelease                           
Hit:11 http://security.ubuntu.com/ubuntu jammy-security InRelease                         
Hit:12 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu jammy InRelease
Hit:13 https://ppa.launchpadcontent.net/obsproject/obs-studio/ubuntu jammy InRelease
Fetched 128 kB in 1s (94,5 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
57 packages can be upgraded. Run 'apt list --upgradable' to see them.
N: Download is performed unsandboxed as root as file '/home/igor/local-apt-repo/./InRelease' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ echo $?
0
```

## Task 2: Simulate Package Installation and Identify Dependencies

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~$ apt-cache showpkg zoom
Package: zoom
Versions: 
6.1.0.198 (/var/lib/apt/lists/_home_igor_local-apt-repo_._Packages)
 Description Language: 
                 File: /var/lib/apt/lists/_home_igor_local-apt-repo_._Packages
                  MD5: 7d0a999457982a32a3b773b302d96329


Reverse Depends: 
Dependencies: 
6.1.0.198 - libglib2.0-0 (0 (null)) libxcb-keysyms1 (0 (null)) libxcb-xinerama0 (0 (null)) libdbus-1-3 (0 (null)) libxcb-shape0 (0 (null)) libxcb-shm0 (0 (null)) libxcb-xfixes0 (0 (null)) libxcb-randr0 (0 (null)) libxcb-image0 (0 (null)) libfontconfig1 (0 (null)) libxi6 (0 (null)) libsm6 (0 (null)) libxrender1 (0 (null)) libpulse0 (0 (null)) libxcomposite1 (0 (null)) libxslt1.1 (0 (null)) libsqlite3-0 (0 (null)) libxcb-xtest0 (0 (null)) libxtst6 (0 (null)) ibus (0 (null)) libxkbcommon-x11-0 (0 (null)) desktop-file-utils (0 (null)) libgbm1 (0 (null)) libdrm2 (0 (null)) libxcb-cursor0 (0 (null)) libxcb-icccm4 (0 (null)) libatomic1 (0 (null)) libfreetype6 (2 2.6) libgbm1 (2 17.1.0~rc2) libegl1-mesa (0 (null)) libgl1-mesa-glx (0 (null)) 
Provides: 
6.1.0.198 - 
Reverse Provides: 

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~$ sudo apt-get install -s zoom
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libegl1-mesa libgl1-mesa-glx libxcb-cursor0 libxcb-xtest0
The following NEW packages will be installed:
  libegl1-mesa libgl1-mesa-glx libxcb-cursor0 libxcb-xtest0 zoom
0 upgraded, 5 newly installed, 0 to remove and 42 not upgraded.
Inst libegl1-mesa (23.0.4-0ubuntu1~22.04.1 Ubuntu:22.04/jammy-updates [amd64])
Inst libgl1-mesa-glx (23.0.4-0ubuntu1~22.04.1 Ubuntu:22.04/jammy-updates [amd64])
Inst libxcb-xtest0 (1.14-3ubuntu3 Ubuntu:22.04/jammy [amd64])
Inst libxcb-cursor0 (0.1.1-4ubuntu1 Ubuntu:22.04/jammy [amd64])
Inst zoom (6.1.0.198 localhost [amd64])
Conf libegl1-mesa (23.0.4-0ubuntu1~22.04.1 Ubuntu:22.04/jammy-updates [amd64])
Conf libgl1-mesa-glx (23.0.4-0ubuntu1~22.04.1 Ubuntu:22.04/jammy-updates [amd64])
Conf libxcb-xtest0 (1.14-3ubuntu3 Ubuntu:22.04/jammy [amd64])
Conf libxcb-cursor0 (0.1.1-4ubuntu1 Ubuntu:22.04/jammy [amd64])
Conf zoom (6.1.0.198 localhost [amd64])
```

## Task 3: Hold and Unhold Package Versions

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~$ sudo apt-mark hold make
make set on hold.

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~$ apt-mark showhold
make

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~$ sudo apt-mark unhold make
Canceled hold on make.

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~$ apt-mark showhold
```