## CentOS 7 VM

The Vagrant file creates a CentOS 7 Docker VM that uses the devicemapper storage driver in a direct-lvm configuration. 

### Usage

#### Run
 1. Download the vagrant file
 ```
 mkdir centos7
 cd centos7
 curl https://raw.githubusercontent.com/sbobylev/docker-direct-lvm/master/Vagrantfile -o Vagrantfile
 ```
 2. Start the VM
 ```
 vagrant up
 
 --- Output ---
 Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'centos/7'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'centos/7' is up to date...
==> default: A newer version of the box 'centos/7' is available! You currently
==> default: have version '1710.01'. The latest is version '1801.02'. Run
==> default: `vagrant box update` to update.
==> default: Setting the name of the VM: centos_default_1518814035152_87628
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
...
 ```
 #### Verify
 
 ```
 vagrant ssh
[vagrant@localhost ~]$ sudo su -
[root@localhost ~]# docker info | grep 'Storage Driver'
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
Storage Driver: devicemapper
[root@localhost ~]#
 ```
