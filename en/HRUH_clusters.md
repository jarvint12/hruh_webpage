# Commands to install softwares

**You need superuser (sudo) privileges for most installing and package commands**  

## apt
  
Apt is a package manager, which install software, remove software and update your system.  
 
### Updating packages

  #### 1. Update package database
  ```bash
  sudo apt update
  ```
  Output lines contains three types of beginnings:
  * Hit: Package already has its latest version
  * Ign: Package was ignored, perhaps because last update was so recently
  * Get: New version available, information about the version is downloaded and size can be found in the end of the line.

  #### 2. Upgrade packages
  After updating, you can upgrade all old versions with
  ```bash
  sudo apt upgrade
  ```
  or in some cases old package is needed to remove before updating, then you can use command
  ```bash
  sudo apt full-upgrade
  ```
  which will take care of everything.

### Get the content of (un)installed package
```bash
apt show <package_name> 
```

### List installed packages
```bash
apt list --installed
```
Could also list upgradeable with ```--upgradeable``` or packages available for system with ```--all-versions```

### Install new packages
```bash
sudo apt install <package_name1> <package_name2> <package_name3>
```
If you are not sure of the package name ending, you can write the beginning of the name and press tab.  
If you try to install existing package, it is not reinstalled, but upgraded if possible. Upgrading can be prevented adding  
```--no-upgrade``` addition to the command.

### Remove packages
```bash
sudo apt remove <package_name>
```
If you want to remove everything related to the package, like configuration files, use
```bash
sudo apt purge <package_name>
```
This can be used to already removed packages, but usually remove is enough for removing package.


### Clean your system from removed packages' help packages
```bash
sudo apt autoremove
```

## yum
Another tool for installing, updating, removing, finding and managing packages and repositories is
```bash
yum
```

### Updating packages
```bash
yum update <package_name>
```

### List installed packages
```bash
yum list installed
```
I would anyway recommend to pipe that command to less (More about navigating in less can be found in the end of page https://linuxize.com/post/less-command-in-linux/. Basically with keyboard arrows. When you want to quit less, type q.) 
```bash
yum list installed | less
```

### List all available packages
```bash
yum list
```
Again, this can be piped to less.

### Get information about package
```bash
yum info <package_name>
```

### Check available updates
```bash
yum check-update
```

### Update system
```bash
yum update
```

### Install packages
```bash
yum install <package_name>
```
After running the command above, you are asked for confirm. Type y for yes.

### Remove packages
```bash
yum remove <package_name>
```

### Clean your system from useless packages
```bash
yum clean all
```

## Installing softwares with make
Unlike with package installers, when you install softwares with make you should keep count which files are installed and where, because package managers are not taking care of them.

### 1. Download tar file
For example mpg123-1.26.1.tar.bz2 from http://www.linuxfromscratch.org/blfs/view/svn/multimedia/mpg123.html
```bash
wget https://downloads.sourceforge.net/mpg123/mpg123-1.26.1.tar.bz2
```

### 2. Unzip tar file
Extracting commands for different tar file types can be found [here](https://how-to.fandom.com/wiki/How_to_untar_a_tar_file_or_gzip-bz2_tar_file). This case (tar.bz2):
```bash
tar -xjf mpg123-1.26.1.tar.bz2
```
Now there should be multiple files or new directory with multiple files, for example README and perhaps INSTALL.

### 3. Read README and/or INSTALL for instructions
Usually installation is done by three steps
* ./configure
* make
* make install

### 4. Run configure
In addition to README, there probably exists 'configure' file (different from for example configure.ac). First step is usually running this file, so if you are in the same directory as the file, just type
```bash
./configure
```

### 5. Compile program with
```bash
make
```
Command takes all the information that was gathered from configuration progress, take the source code and compile it for you. Make does not need any arguments. This can take a time.

### 6. Run
```bash
sudo make install
```

### 7. Check everything went fine
```bash
which mpg123
```
Gives you location for installed tool, this time mpg123.

```bash
mpg123 --help
```
Should give you help page of that command
### 6. Errors
After installing and trying to run:  
```mpg123: error while loading shared libraries: libmpg123.so.0: cannot open shared object file: No such file or directory```
You can run ```sudo ldconfig``` which should help.


