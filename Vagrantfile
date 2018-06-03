# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
  config.vm.define :nodo_1 do |server|
    server.vm.box = "centos/7"
    server.vm.network :private_network, ip: "192.168.131.15"
    server.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "8", "--name", "nodo_1" ]
    end
   server.vm.provision "shell", inline: <<-SHELL
       sudo yum -y remove docker
       sudo yum -y remove docker-selinux
       sudo rpm --import "https://sks-keyservers.net/pks/lookup?op=get&search=0xee6d536cf7dc86e2d7d56f59a178ac6c6238f52e"
       sudo yum install -y yum-utils
       sudo yum-config-manager --add-repo https://packages.docker.com/1.13/yum/repo/main/centos/7
       sudo yum makecache fast
       sudo yum -y install docker-engine
       sudo systemctl start docker
       sudo usermod -aG docker vagrant
    SHELL
  end
end


