# Testing Packer builds #

To build these, first initialize the repository and enter the Vagrant environment:

```
git submodule update --init --recursive
vagrant up && vagrant ssh
$ cd /sync
```

# boxcutter Ubuntu 16.04 #

[boxcutter/ubuntu](https://github.com/boxcutter/ubuntu):

```
vagrant@vagrant-ubuntu-wily-64:~$ cd /sync/boxcutter-ubuntu
vagrant@vagrant-ubuntu-wily-64:/sync/boxcutter-ubuntu$ packer build --only=virtualbox-iso -var-file=ubuntu1604.json -var "headless=true" ubuntu.json
virtualbox-iso output will be in this color.

==> virtualbox-iso: Downloading or copying Guest additions
    virtualbox-iso: Downloading or copying: file:///usr/share/virtualbox/VBoxGuestAdditions.iso
==> virtualbox-iso: Downloading or copying ISO
    virtualbox-iso: Downloading or copying: file:///Volumes/Storage/software/ubuntu/ubuntu-16.04-server-amd64.iso
    virtualbox-iso: Error downloading: open /Volumes/Storage/software/ubuntu/ubuntu-16.04-server-amd64.iso: no such file or directory
    virtualbox-iso: Downloading or copying: http://releases.ubuntu.com/16.04/ubuntu-16.04-server-amd64.iso
==> virtualbox-iso: Creating floppy disk...
    virtualbox-iso: Copying: http/preseed.cfg
==> virtualbox-iso: Creating virtual machine...
==> virtualbox-iso: Creating hard drive...
==> virtualbox-iso: Attaching floppy disk...
==> virtualbox-iso: Creating forwarded port mapping for communicator (SSH, WinRM, etc) (host port 4358)
==> virtualbox-iso: Executing custom VBoxManage commands...
    virtualbox-iso: Executing: modifyvm ubuntu1604 --memory 512
    virtualbox-iso: Executing: modifyvm ubuntu1604 --cpus 1
==> virtualbox-iso: Starting the virtual machine...
    virtualbox-iso: The VM will be run headless, without a GUI. If you want to
    virtualbox-iso: view the screen of the VM, connect via VRDP without a password to
    virtualbox-iso: 127.0.0.1:5990
==> virtualbox-iso: Waiting 10s for boot...
==> virtualbox-iso: Typing the boot command...
==> virtualbox-iso: Waiting for SSH to become available...
```

(waits indefinitely)

# geerlingguy CentOS 7 #

[geerlingguy/packer-centos-7](https://github.com/geerlingguy/packer-centos-7/):

```
vagrant@vagrant-ubuntu-wily-64:~$ cd /sync/geerlingguy-centos-7
vagrant@vagrant-ubuntu-wily-64:/sync/geerlingguy-centos-7$ sudo ansible-galaxy install -r requirements.txt
vagrant@vagrant-ubuntu-wily-64:/sync/geerlingguy-centos7$ packer build --only=virtualbox-iso centos7.json
virtualbox-iso output will be in this color.

==> virtualbox-iso: Downloading or copying Guest additions
    virtualbox-iso: Downloading or copying: file:///usr/share/virtualbox/VBoxGuestAdditions.iso
==> virtualbox-iso: Downloading or copying ISO
    virtualbox-iso: Downloading or copying: file:///CentOS-7-x86_64-Minimal-1511.iso
    virtualbox-iso: Error downloading: open /CentOS-7-x86_64-Minimal-1511.iso: no such file or directory
    virtualbox-iso: Downloading or copying: http://centos.mirrors.hoobly.com/7/isos/x86_64/CentOS-7-x86_64-Minimal-1511.iso
==> virtualbox-iso: Starting HTTP server on port 8715
==> virtualbox-iso: Creating virtual machine...
==> virtualbox-iso: Creating hard drive...
==> virtualbox-iso: Creating forwarded port mapping for communicator (SSH, WinRM, etc) (host port 4021)
==> virtualbox-iso: Executing custom VBoxManage commands...
    virtualbox-iso: Executing: modifyvm packer-centos-7-x86_64 --memory 512
    virtualbox-iso: Executing: modifyvm packer-centos-7-x86_64 --cpus 2
==> virtualbox-iso: Starting the virtual machine...
    virtualbox-iso: The VM will be run headless, without a GUI. If you want to
    virtualbox-iso: view the screen of the VM, connect via VRDP without a password to
    virtualbox-iso: 127.0.0.1:5925
==> virtualbox-iso: Error starting VM: VBoxManage error:
==> virtualbox-iso: Unregistering and deleting virtual machine...
==> virtualbox-iso: Deleting output directory...
Build 'virtualbox-iso' errored: Error starting VM: VBoxManage error:

==> Some builds didn't complete successfully and had errors:
--> virtualbox-iso: Error starting VM: VBoxManage error:

==> Builds finished but no artifacts were created.
```

# geerlingguy Ubuntu 14.04 #

[geerlingguy/packer-ubuntu-1404](https://github.com/geerlingguy/packer-ubuntu-1404):

```
vagrant@vagrant-ubuntu-wily-64:~$ cd /sync/geerlingguy-ubuntu-1404
vagrant@vagrant-ubuntu-wily-64:/sync/geerlingguy-ubuntu-1404$ sudo ansible-galaxy install -r requirements.txt
vagrant@vagrant-ubuntu-wily-64:/sync/geerlingguy-ubuntu-1404$ packer build --only=virtualbox-iso ubuntu1404.json
virtualbox-iso output will be in this color.

==> virtualbox-iso: Downloading or copying Guest additions
    virtualbox-iso: Downloading or copying: file:///usr/share/virtualbox/VBoxGuestAdditions.iso
==> virtualbox-iso: Downloading or copying ISO
    virtualbox-iso: Downloading or copying: file:///iso/ubuntu-14.04.1-server-amd64.iso
    virtualbox-iso: Error downloading: open /iso/ubuntu-14.04.1-server-amd64.iso: no such file or directory
    virtualbox-iso: Downloading or copying: http://old-releases.ubuntu.com/releases/14.04.1/ubuntu-14.04.1-server-amd64.iso
==> virtualbox-iso: Starting HTTP server on port 8958
==> virtualbox-iso: Creating virtual machine...
==> virtualbox-iso: Creating hard drive...
==> virtualbox-iso: Creating forwarded port mapping for communicator (SSH, WinRM, etc) (host port 3696)
==> virtualbox-iso: Executing custom VBoxManage commands...
    virtualbox-iso: Executing: modifyvm packer-ubuntu-14.04-amd64 --memory 512
    virtualbox-iso: Executing: modifyvm packer-ubuntu-14.04-amd64 --cpus 2
==> virtualbox-iso: Starting the virtual machine...
    virtualbox-iso: The VM will be run headless, without a GUI. If you want to
    virtualbox-iso: view the screen of the VM, connect via VRDP without a password to
    virtualbox-iso: 127.0.0.1:5983
==> virtualbox-iso: Error starting VM: VBoxManage error:
==> virtualbox-iso: Unregistering and deleting virtual machine...
==> virtualbox-iso: Deleting output directory...
Build 'virtualbox-iso' errored: Error starting VM: VBoxManage error:

==> Some builds didn't complete successfully and had errors:
--> virtualbox-iso: Error starting VM: VBoxManage error:

==> Builds finished but no artifacts were created.
```
