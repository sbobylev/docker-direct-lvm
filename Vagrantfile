# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|  
  config.vm.box = "centos/7"
  docker_storage = './docker_direct_lvm.vdi'
  config.vm.provider "virtualbox" do |vb|
    if not File.exists?(docker_storage)
      vb.customize ['createhd', '--filename', docker_storage, '--variant', 'Fixed', '--size', 30 * 1024]
    end
    vb.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', docker_storage]
  end

  config.vm.synced_folder ".", "/vagrant", type: "rsync",
    rsync__exclude: ["*.vdi", ".git", "README.md"]

  config.vm.provision "shell", inline: <<-SHELL
    echo ",,8e;" | sudo sfdisk  /dev/sdb
    partprobe /dev/sdb
    vgcreate docker-vg /dev/sdb1
    sudo yum install -y docker
    echo 'VG=docker-vg' | tee -a /etc/sysconfig/docker-storage-setup 
    echo 'SETUP_LVM_THIN_POOL=yes' | tee -a /etc/sysconfig/docker-storage-setup
    echo 'DATA_SIZE=90%FREE' | tee -a /etc/sysconfig/docker-storage-setup
    /bin/docker-storage-setup
    sudo systemctl enable docker
    sudo systemctl start docker
  SHELL
end  
