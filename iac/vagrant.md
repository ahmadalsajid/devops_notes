[Home](../README.md)

#### Vagrant
**Prerequisites**  
Install [VirtualBox](https://www.virtualbox.org/)  

**Installation**  
To install Vagrant, first find the [appropriate package](https://www.vagrantup.com/downloads) 
for your system and download it. Vagrant is packaged as an operating-specific 
package. Run the installer for your system. The installer will automatically 
add vagrant to your system path so that it is available in terminals.  

Check Vagrant
```
$ vagrant
```
> Some operating system distributions include a vagrant package in their upstream 
> package repos. **Please do not install Vagrant in this manner.** Typically 
> these packages are missing dependencies or include very outdated versions of 
> Vagrant. If you install via your system's package manager, it is very likely 
> that you will experience issues. Please use the official installers on the downloads page.

**Quick start**  
Initialize Vagrant.
```
$ vagrant init hashicorp/bionic64
```
Start the virtual machine.
```
$ vagrant up
```
SSH into this machine with vagrant ssh, and explore your environment. Leave the 
SSH session with `logout`. When you are done exploring terminate the virtual 
machine, and confirm when the CLI prompts you by typing yes.
```
$ vagrant destroy
```

#### References: 
* [Vagrant documentation](https://learn.hashicorp.com/collections/vagrant/getting-started) 
