# DevOps Lab 4
## Task 1: Configure and Use a Local Package Repository
### The output:
```bash
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ mkdir -p ~/local-apt-repo
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ cp jdk-19.0.2_linux-x64_bin.deb ~/local-apt-repo/
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ mkdir -p ~/local-apt-repo
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ cp jdk-19.0.2_linux-x64_bin.deb ~/local-apt-repo/
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   jdk-19
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ ls ~/local-apt-repo/
Packages.gz  jdk-19.0.2_linux-x64_bin.deb
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ echo "deb [trusted=yes] file:/home/roiven/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
deb [trusted=yes] file:/home/roiven/local-apt-repo ./
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ sudo apt update
Get:1 file:/home/roiven/local-apt-repo ./ InRelease
Ign:1 file:/home/roiven/local-apt-repo ./ InRelease
Get:2 file:/home/roiven/local-apt-repo ./ Release
Ign:2 file:/home/roiven/local-apt-repo ./ Release
Get:3 file:/home/roiven/local-apt-repo ./ Packages
Ign:3 file:/home/roiven/local-apt-repo ./ Packages
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Ign:4 file:/home/roiven/local-apt-repo ./ Translation-en
Get:3 file:/home/roiven/local-apt-repo ./ Packages
Ign:3 file:/home/roiven/local-apt-repo ./ Packages
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Ign:4 file:/home/roiven/local-apt-repo ./ Translation-en
Get:3 file:/home/roiven/local-apt-repo ./ Packages
Ign:3 file:/home/roiven/local-apt-repo ./ Packages
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Ign:4 file:/home/roiven/local-apt-repo ./ Translation-en
Get:3 file:/home/roiven/local-apt-repo ./ Packages [616 B]
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Err:4 file:/home/roiven/local-apt-repo ./ Translation-en
  File not found - /home/roiven/local-apt-repo/./en.gz (2: No such file or directory)
Ign:3 file:/home/roiven/local-apt-repo ./ Packages
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Ign:4 file:/home/roiven/local-apt-repo ./ Translation-en
Get:3 file:/home/roiven/local-apt-repo ./ Packages
Ign:3 file:/home/roiven/local-apt-repo ./ Packages
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Ign:4 file:/home/roiven/local-apt-repo ./ Translation-en
Get:3 file:/home/roiven/local-apt-repo ./ Packages
Ign:3 file:/home/roiven/local-apt-repo ./ Packages
Get:4 file:/home/roiven/local-apt-repo ./ Translation-en
Ign:4 file:/home/roiven/local-apt-repo ./ Translation-en
Get:3 file:/home/roiven/local-apt-repo ./ Packages
Err:3 file:/home/roiven/local-apt-repo ./ Packages
  File not found - /home/roiven/local-apt-repo/./Packages (2: No such file or directory)
Get:5 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
Hit:6 http://archive.ubuntu.com/ubuntu jammy InRelease                             
Get:7 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
Get:8 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [1526 kB]
Hit:9 http://archive.ubuntu.com/ubuntu jammy-backports InRelease  
Get:10 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1736 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy-updates/main Translation-en [319 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [2000 kB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/restricted Translation-en [340 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1088 kB]
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/universe Translation-en [251 kB]
Fetched 7517 kB in 3s (2597 kB/s)
Reading package lists... Done
N: Download is performed unsandboxed as root as file '/home/roiven/local-apt-repo/./InRelease' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)
E: Failed to fetch file:/home/roiven/local-apt-repo/./Packages  File not found - /home/roiven/local-apt-repo/./Packages (2: No such file or directory)
E: Some index files failed to download. They have been ignored, or old ones used instead.

```