# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu1404"
  config.vm.network :private_network, type: :dhcp

  # gem install bundler runs out of memory on 512MB.  
  config.vm.provider 'virtualbox' do |v|
    v.memory = 1024
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'provisioning/logstash-dev.yml'
  end
end