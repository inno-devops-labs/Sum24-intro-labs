
# Task 1: Configure and Use a Local Package Repository

## Step-by-Step Setup and Installation

### Create a Local Repository

```sh
mkdir -p ~/local-apt-repo
cp /path/to/nano_5.4-2_amd64.deb ~/local-apt-repo/
```

### Generate the Package Index

```sh
dpkg-scanpackages ~/local-apt-repo | gzip -c > ~/local-apt-repo/Packages.gz
```

### Add the Local Repository to Your Sources List

```sh
echo "deb [trusted=yes] file:/home/aakindeko/local-apt-repo ./" | sudo tee -a /etc/apt/sources.list
sudo apt update
```

### Install a Package from the Local Repository

```sh
sudo apt install nano
```

### Output and Verification

```sh
# Output of sudo apt install nano
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  nano
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B/241 kB of archives.
After this operation, 1,147 kB of additional disk space will be used.
Selecting previously unselected package nano.
(Reading database ... 305696 files and directories currently installed.)
Preparing to unpack .../nano_5.4-2_amd64.deb ...
Unpacking nano (5.4-2) ...
Setting up nano (5.4-2) ...
update-alternatives: using /bin/nano to provide /usr/bin/editor (editor) in auto mode
```

# Task 2: Package Installation and Identify Dependencies

## Package Installation

### Show Package Information

```sh
apt-cache showpkg curl
```

### Installation

```sh
sudo apt-get install curl
```

### Dependencies and Packages

- **Dependencies**:
  ```sh
  # Output of sudo apt-get install curl
  Reading package lists... Done
  Building dependency tree       
  Reading state information... Done
  The following additional packages will be installed:
    libcurl4
  Suggested packages:
    curl-doc
  The following NEW packages will be installed:
    curl libcurl4
  0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
  Inst libcurl4 (7.68.0-1ubuntu2.6 Ubuntu:20.04/focal-updates [amd64])
  Inst curl (7.68.0-1ubuntu2.6 Ubuntu:20.04/focal-updates [amd64])
  Conf libcurl4 (7.68.0-1ubuntu2.6 Ubuntu:20.04/focal-updates [amd64])
  Conf curl (7.68.0-1ubuntu2.6 Ubuntu:20.04/focal-updates [amd64])
  ```

- **Packages to be Installed**:
  ```sh
  curl
  libcurl4
  ```

# Task 3: Hold and Unhold Package Versions

## Holding and Unholding a Package

### Install a Package

```sh
sudo apt install vim
```

### Hold the Package

```sh
sudo apt-mark hold vim
```

### Verify the Hold Status

```sh
apt-mark showhold
```

### Unhold the Package

```sh
sudo apt-mark unhold vim
```

### Verification and Output

- **Hold Status**:
  ```sh
  # Output of apt-mark showhold
  vim
  ```

- **Unhold Status**:
  ```sh
  # Output after unholding the package
  vim
  ```

