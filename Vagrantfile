# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.define "couchbase01" do |couchbase01|
    couchbase01.vm.box = "mrlesmithjr/trusty64"
    couchbase01.vm.hostname = "couchbase01"

    couchbase01.vm.network :private_network, ip: "192.168.202.201"
    couchbase01.vm.network :forwarded_port, guest: 8091, host: 8091

    couchbase01.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
  end
  config.vm.define "couchbase02" do |couchbase02|
    couchbase02.vm.box = "mrlesmithjr/trusty64"
    couchbase02.vm.hostname = "couchbase02"

    couchbase02.vm.network :private_network, ip: "192.168.202.202"

    couchbase02.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
  end  
  config.vm.provision :shell, path: "provision.sh", keep_color: "true"
  config.vm.provision :shell, inline: 'ansible-galaxy install -r /vagrant/requirements.yml -f'
  config.vm.provision :shell, inline: 'ansible-playbook -i /vagrant/hosts -c local /vagrant/playbook.yml'
end