# Task 1

## Create a Local Repository:
```shell
aslan@aslan-X756UXM:~$ mkdir -p ~/custom-repo
aslan@aslan-X756UXM:~$ cp /home/aslan/Downloads/TL.deb ~/custom-repo
```

## Generate the Package Index:
```shell
aslan@aslan-X756UXM:~$ dpkg-scanpackages ~/custom-repo | gzip -c > ~/custom-repo/Packages.gz 
dpkg-scanpackages: info: Wrote 1 entries to output Packages file.

```

## Add the Local Repository to Your Sources List:
```shell
aslan@aslan-X756UXM:~$ echo "deb [trusted=yes] file:/home/aslan/custom-repo ./" | sudo tee -a /etc/apt/sources.list
deb [trusted=yes] file:/home/aslan/custom-repo ./
```
sudo apt update

```shell
Get:7 file:/home/aslan/custom-repo ./ Packages                                             
Err:7 file:/home/aslan/custom-repo ./ Packages                                                  
  File not found - /home/aslan/custom-repo/./Packages (2: No such file or directory)

```

## Install a Package from the Local Repository:

```shell
aslan@aslan-X756UXM:~$ sudo apt install custom-repo
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package custom-repo

```
