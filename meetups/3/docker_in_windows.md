# Installing and using Docker in a Windows host

This readme file describes the various alternatives that one can follow to have a working Docker environment if their host system is Windows.

## 1. Using Docker Machine (recommended)
Prerequisites: More time compared to option #2
When to follow: When you want to directly develop on the host and be able to seamlessly inject your code in the new images you create

Please check our extensive guide [here](docker_machine_windows/README.md)

## 2. Using our preconfigured VM export
Prerequisite: Virtualbox
When to follow: If you are comfortable working with vim/nano, you have an IDE that supports remote editing, or want to configure a shared folder among the host and the guest system.

A very easy way to set up the environment is to use our [preconfigured OVA file](https://www.dropbox.com/s/ejxk0vrc69jr5pp/meetup.ova?dl=0) and import that into Virtualbox (File->Import Appliance-><Fill in the path to the OVA file>). You should then configure the port forwarding rules to add a new one for SSH (right click on the VM->Settings->Network->Advanced->Port Forwarding->Host port 22222, Guest port:22). You can then directly connect to your guest by connecting to localhost:22222 via your SSH client of choice. You can either edit files using vim, or using an IDE with remote editing capabilities, like Eclipse, or add a shared folder among the host and the guest (right click on the VM->Shared folders).

## 3. By creating the environment on your own
Prerequisite: Some extra time
When to follow: If you want to install Docker on your own

The high-level steps are:
1. Download an Ubuntu ISO and install it in a new VM
2. `sudo apt-get update`
3. Download, `chmod` and run the [docker installation script](https://get.docker.com/)
4. Run `sudo usermod -aG docker $USER` to not have to use `sudo` prior to every docker command
