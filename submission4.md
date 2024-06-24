# Lab 4

## Task 1
1. After creating a local directory, I placed a ```.deb``` package in it (I chose [OBS latest release](https://github.com/obsproject/obs-studio/releases) ```.deb``` package)
```
$ mkdir -p ~/local-apt-repo
$ cp ~/OBS-Studio-30.1.2-Ubuntu-x86_64.deb ~/local-apt-repo/

```
2. Generating the Packages.gz file
```
$ dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz

dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   obs-studio
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.

```
3. Adding the repository to the ```sources.list```
After adding the repository to the sources list and updating my package was among the first one in the list:
```
$ sudo apt update

Get:1 file:/home/mango/local-apt-repo ./ InRelease
Ign:1 file:/home/mango/local-apt-repo ./ InRelease
Get:2 file:/home/mango/local-apt-repo ./ Release
Ign:2 file:/home/mango/local-apt-repo ./ Release
Get:3 file:/home/mango/local-apt-repo ./ Packages
Ign:3 file:/home/mango/local-apt-repo ./ Packages
Get:4 file:/home/mango/local-apt-repo ./ Translation-en_US
Ign:4 file:/home/mango/local-apt-repo ./ Translation-en_US
...
```

4. Verifying the contents
Firstly, verify the contents of the Packages.gz file
```
$ zcat Packages.gz

Package: obs-studio
Version: 30.1.2-1
Architecture: amd64
Maintainer: OBS Project
Installed-Size: 286070
Depends: libasound2 (>= 1.0.16), libatk-bridge2.0-0 (>= 2.5.3), ... <other dependencies ommitted to not cluter the report>
Filename: /home/mango/local-apt-repo/OBS-Studio-30.1.2-Ubuntu-x86_64.deb
Size: 114411528
MD5sum: fd6a8d56950aed91ba48b561daae6a5f
SHA1: 771a824417d0b0a608f9c6bcecb9d71ec36e2efd
SHA256: d27fc564b6e9fd7ef6219b5c6b06e04743978e910d461714f4885265767155ab
Section: devel
Priority: optional
Description: Free and open source software for video recording and live streaming

```
Next, information about the package repository:
```
$ apt policy local-apt-repository 

local-apt-repository:
  Installed: (none)
  Candidate: 0.6
  Version table:
     0.6 500
        500 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 Packages
        500 http://ru.archive.ubuntu.com/ubuntu focal/universe i386 Packages
```
5. Finally, install the package:
```
$ sudo apt install local-apt-repository 

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  local-apt-repository
0 upgraded, 1 newly installed, 0 to remove and 14 not upgraded.
Need to get 5 888 B of archives.
After this operation, 33,8 kB of additional disk space will be used.
Get:1 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 local-apt-repository all 0.6 [5 888 B]
Fetched 5 888 B in 0s (51,6 kB/s)                    
Selecting previously unselected package local-apt-repository.
(Reading database ... 258607 files and directories currently installed.)
Preparing to unpack .../local-apt-repository_0.6_all.deb ...
Unpacking local-apt-repository (0.6) ...
Setting up local-apt-repository (0.6) ...
Created symlink /etc/systemd/system/paths.target.wants/local-apt-repository.path → /lib/systemd/system/local-apt-repository.path.

```
## Task 2
1. Choose a package for installation

A ROS-noetic pinocchio package was chosen for simulation. Reference (link)[https://index.ros.org/p/pinocchio/]

### Dependencies

```
$ apt-cache showpkg ros-noetic-pinocchio

...
Dependencies: 
2.6.21-1focal.20240612.144539 - libboost-chrono1.71.0 (0 (null)) libboost-filesystem1.71.0 (0 (null)) libboost-python1.71.0 (0 (null)) libboost-python1.71.0-py38 (0 (null)) libboost-serialization1.71.0 (0 (null)) libboost-system1.71.0 (0 (null)) libc6 (2 2.14) libconsole-bridge0.4 (0 (null)) libgcc-s1 (2 3.0) libstdc++6 (2 9) liburdfdom-model (0 (null)) liburdfdom-model-state (0 (null)) liburdfdom-sensor (0 (null)) liburdfdom-world (0 (null)) ros-noetic-octomap (0 (null)) libboost-all-dev (0 (null)) libeigen3-dev (0 (null)) liburdfdom-dev (0 (null)) python3-dev (0 (null)) python3-numpy (0 (null)) ros-noetic-catkin (0 (null)) ros-noetic-eigenpy (0 (null)) ros-noetic-hpp-fcl (0 (null)) 
...

```
### Packages that would be installed
```
$ sudo apt-get install -s ros-noetic-pinocchio

...
The following additional packages will be installed:
  liblbfgsb0 python3-decorator python3-scipy ros-noetic-eigenpy ros-noetic-hpp-fcl ros-noetic-octomap
Suggested packages:
  python-scipy-doc
The following NEW packages will be installed:
  liblbfgsb0 python3-decorator python3-scipy ros-noetic-eigenpy ros-noetic-hpp-fcl ros-noetic-octomap ros-noetic-pinocchio
```
Below is the package installation simulation, including their respective **versions**
```
Inst liblbfgsb0 (3.0+dfsg.3-7build1 Ubuntu:20.04/focal [amd64])
Inst python3-decorator (4.4.2-0ubuntu1 Ubuntu:20.04/focal [all])
Inst python3-scipy (1.3.3-3build1 Ubuntu:20.04/focal [amd64])
Inst ros-noetic-eigenpy (3.7.0-1focal.20240612.130817 ROS focal:focal [amd64])
Inst ros-noetic-octomap (1.9.8-1focal.20220514.014451 ROS focal:focal [amd64])
Inst ros-noetic-hpp-fcl (2.4.4-1focal.20240612.135941 ROS focal:focal [amd64])
Inst ros-noetic-pinocchio (2.6.21-1focal.20240612.144539 ROS focal:focal [amd64])
```

## Task 3
One example of a package on Ubuntu 20.04 that updates frequently is the VS Code (```code```)

1. Hold the package
```
$ sudo apt-mark hold code

code set on hold.
```
Verifying the held packages:
```
$ apt-mark showhold

code
```

2. Unhold package
```
$ sudo apt-mark unhold code

Canceled hold on code.

```