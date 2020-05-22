# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :webdb do |webdb|
    webdb.vm.box = "bento/centos-7.3"
    webdb.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
    webdb.vm.network "private_network", ip: "192.168.10.10"
    webdb.vm.synced_folder "./vm/ansible", "/home/vagrant/ansible", group: "vagrant", mount_options: ["dmode=775", "fmode=775"]
    webdb.vm.provider "virtualbox" do |vb|
      vb.name = "ansible_sample"
      vb.memory = "2048"
    end

    # 初回のみ実行
    webdb.vm.provision "shell", inline: <<-SHELL
      sudo yum -y install epel-release;
      sudo yum -y install ansible;
      cd ansible;
      ansible-playbook -i hosts -c local playbook.yml;
    SHELL
  end
end
