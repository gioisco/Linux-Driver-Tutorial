# Linux-Driver-Tutorial
How to create a linux driver from scratch


## Prerequisites

### Update your packages

Run the following command to update and upgrade your system:

```bash
sudo apt update && sudo apt upgrade
```

### Install required packages (I use `Pop!_OS`)

> **Tip:** To check if a package is already installed, you can use:

 - `apt list -i <package-name>`  
   or  
 - `apt-cache policy <package-name>`

#### Install Kernel Headers

```bash
sudo apt install linux-headers-$(uname -r)
```

#### Install Build Essentials (includes GCC, Make, etc.)

```bash
sudo apt install build-essential
```

> **Important:** Reboot your system if a new kernel was installed during the update.


## Create a module

[01. Create your first Hello World Kernel Driver](01_hello/Create_Hello_World_Linux_Driver.md)
