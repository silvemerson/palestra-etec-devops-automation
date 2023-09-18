# -*- mode: ruby -*-
# vi: set ft=ruby :

vms = {
  "tools-etec" => {"memory"=>"6144" , "cpus"=>"2", "ip" => "20" , 'box' => 'silvemerson/ubuntu-20-04-ansible', 'provision' => 'provision/ansible/tools.yml' }
}

Vagrant.configure("2") do |config|
    
  vms.each do |name, conf|
    config.vm.define "#{name}" do |k|
      k.vm.box = "#{conf['box']}"
      k.vm.hostname = "#{name}"
      k.vm.network 'private_network', ip: "192.168.56.#{conf['ip']}"
      k.vm.provider 'virtualbox' do |vb|
        vb.memory = conf['memory']
        vb.cpus = conf['cpus']
      end
      k.vm.provision 'ansible_local' do |ansible|
        ansible.playbook = "#{conf['provision']}"
        ansible.compatibility_mode = '2.0'
      end
    end
  end
end