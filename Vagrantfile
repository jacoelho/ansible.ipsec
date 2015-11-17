# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes = [
  {
    :name => "host1",
    :eth1 => "192.168.205.10",
    :mem => "256",
    :cpu => "1"

  },
  {
    :name => "host2",
    :eth1 => "192.168.205.11",
    :mem => "256",
    :cpu => "1"

  },
  {
    :name => "host3",
    :eth1 => "192.168.205.12",
    :mem => "256",
    :cpu => "1"
  }
]

Vagrant.configure(2) do |config|
  config.vm.box = "boxcutter/ubuntu1404"
  config.vbguest.auto_update = false

  boxes.each do |opts|
    config.vm.define opts[:name] do |cfg|
      cfg.vm.hostname = opts[:name]

      cfg.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", opts[:mem]]
        v.customize ["modifyvm", :id, "--cpus", opts[:cpu]]
      end

      cfg.vm.network :private_network, ip: opts[:eth1], nictype: "virtio"

      cfg.vm.provision :shell, :inline => <<-END
        command -v bats >/dev/null 2>&1 || {
          apt-get install -qq -y software-properties-common
          add-apt-repository ppa:duggan/bats --yes
          apt-get update -qq
          apt-get install -qq -y bats
        }
        #/vagrant/tests/check.bats
      END

      cfg.vm.provision "ansible" do |ansible|
        ansible.playbook = "tests/playbook.yml"
        ansible.verbose = "vvvv"
      end

    end
  end
end
