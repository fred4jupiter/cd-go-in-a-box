# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 8153, host: 8153
  config.vm.network "forwarded_port", guest: 8154, host: 8154
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
	vb.customize ["modifyvm", :id, "--cpus", "4"]
  end
  config.vm.provision "shell", inline: "apt-get update && apt-get upgrade -y && apt-get install -y git && apt-get install -y dos2unix"  
  config.vm.provision "shell", path: "fig-install.sh"
  config.vm.provision "docker" do |d|
	d.run "crosbymichael/skydns",
		args: "-p 172.17.42.1:53:53/udp --name skydns crosbymichael/skydns -nameserver 8.8.8.8:53 -domain docker"
	d.run "crosbymichael/skydock",
		args: "-v /var/run/docker.sock:/docker.sock --name skydock crosbymichael/skydock -ttl 30 -environment dev -s /docker.sock -domain docker -name skydns"
  end  
  config.vm.provision "shell", inline: "cd /vagrant && fig up -d"  
end
