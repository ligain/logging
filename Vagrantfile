# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :web => {
    :box_name => "centos/7",
    :ip_addr => "192.168.11.101",
    :box_version => "1905.1",
    :memory => "512"
  },
  :log => {
    :box_name => "centos/7",
    :ip_addr => "192.168.11.102",
    :box_version => "1905.1",
    :memory => "512"
  }
}

Vagrant.configure("2") do |config|

  MACHINES.each_with_index do |(boxname, boxconfig), idx|

    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.box_version = boxconfig[:box_version]
      box.vm.host_name = boxname.to_s

      box.vm.network "private_network", ip: boxconfig[:ip_addr]
      box.ssh.forward_agent = true

      box.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", boxconfig[:memory]]
      end

      # Execute ansible provisioner after all machines are up and running
      if idx == MACHINES.length - 1
        box.vm.provision "ansible" do |ansible|
          ansible.host_vars = MACHINES
          ansible.playbook = "playbook.yml"
          ansible.compatibility_mode = "2.0"
          ansible.limit = "all"
        end
      end

    end
  end
end
