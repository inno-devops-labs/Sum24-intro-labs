# Software Distribution

## Task 1: Configure and Use a Local Package Repository (`example with discord`)

**Objective**: Set up a local package repository and use it to install packages.

### Download discord.deb

```sh
wget -O discord.deb "https://discordapp.com/api/download?platform=linux&format=deb"
```

### Install `dpkg-dev`

```sh
sudo apt install dpkg-dev
```

### Create a Local Repository

Create a directory to hold your repository and place the `discord.deb` file in it.

```sh
mkdir -p ~/local-apt-repo
cp /path/to/discord.deb ~/local-apt-repo/
```

### Generate the Package Index

Use `dpkg-scanpackages` to create a `Packages` file. Compress this file into a `Packages.gz` archive.

```sh
dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
```

### Add the Local Repository to Your Sources List

Add the repository to your `sources.list`.

> Make sure to update your username in the command below

```sh
echo "deb [trusted=yes] file:/home/yourusername/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
sudo apt update
```

> If you encounter an error like `E: Failed to fetch file:...` verify the `Filename` in the next step and make sure its a relative path e.g. `./discord.deb`

### Verify the Contents of the `Packages.gz` File

- Check that the Packages.gz file contains the correct path and ### metadata for your `discord.deb` filit must be relative path li`./discord.deb`\*\*. Also you can see the package name there. Then check the repository of your package, make sure it's local one.

```sh
zcat Packages.gz
apt policy discord
```

### Install the Package from the Local Repository

- Install the `discord` package using `apt` from your local repository.

```sh
sudo apt install discord
```

- [reference 1](./apt-repository-1.png)
- [reference 2](./apt-repository-2.png)
- [reference 3](./apt-repository-3.png)

## Task 2: Simulate Package Installation and Identify Dependencies

**Dependencies:** The current discord package depends on the following packages (with their versions)

- libayatana-indicator7 (0.9.3-1 Debian:12.5/stable [amd64])
- libdbusmenu-gtk4 (18.10.20180917~bzr492+repack1-3 Debian:12.5/stable [amd64])
- libayatana-appindicator1 (0.5.92-1 Debian:12.5/stable [amd64])

[reference 1](./simulate.png)

## Task 3: Hold and Unhold `discord`

**Objective**: Prevent `discord` package from being upgraded and then allow it to be upgraded again.

### Install the `discord` package

- Install `discord` package from your local repository

```sh
sudo apt install discord
```

### Hold the Package

- Use `apt-mark` to hold the package.

```sh
sudo apt-mark hold discord
```

### Verify the Hold Status

- Check the status of held packages.

```sh
apt-mark showhold
```

### Unhold the Package

- Use `apt-mark` to unhold the package.

```sh
sudo apt-mark unhold discord
```

[reference 1](./hold-package.png)
