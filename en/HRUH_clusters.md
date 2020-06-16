# Commands to install softwares

## apt
**You need superuser (sudo) privileges for most apt commands**  
  
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

##yum
