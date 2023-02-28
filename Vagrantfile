# vi: set ft=ruby :
# -*- mode: ruby -*-

Vagrant.configure("2") do |config|

  require 'yaml'

  if File.file?('values.yaml')
    conf = YAML.load_file('values.yaml')
  else
    raise "Configuration file 'values.yaml' does not exist"
  end

  conf['machines'].each do | name, ip, memory, cpus, box |
    config.vm.define name do |vm|
      vm.vm.box = box||conf['box']
      vm.vm.hostname = name
      vm.vm.boot_timeout = 600
      vm.vm.network :private_network, ip: ip
      vm.vm.provider "virtualbox" do |v|
        v.memory = memory || '256'
    	  v.cpus = cpus || '1'
    	  v.name = name
#        v.customize ['modifyvm',:id,'--nested-hw-virt','on']
      end
    end
  end
end
