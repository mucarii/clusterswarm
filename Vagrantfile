# Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "master" do |master|
    master.vm.network "private_network", ip: "192.168.33.10"
    master.vm.hostname = "master"
    master.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y docker.io
      sudo systemctl start docker
      sudo systemctl enable docker
      # Instalar Vagrant (não é comum)
      wget https://releases.hashicorp.com/vagrant/2.3.4/vagrant_2.3.4_linux_amd64.zip
      unzip vagrant_2.3.4_linux_amd64.zip
      sudo mv vagrant /usr/local/bin/
    SHELL
  end

  (1..3).each do |i|
    config.vm.define "node#{i.to_s.rjust(2, '0')}" do |node|
      node.vm.network "private_network", ip: "192.168.33.1#{i}"
      node.vm.hostname = "node#{i.to_s.rjust(2, '0')}"
      node.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        sudo apt-get install -y docker.io
        sudo systemctl start docker
        sudo systemctl enable docker
        # Instalar Vagrant (não é comum)
        wget https://releases.hashicorp.com/vagrant/2.3.4/vagrant_2.3.4_linux_amd64.zip
        unzip vagrant_2.3.4_linux_amd64.zip
        sudo mv vagrant /usr/local/bin/
      SHELL
    end
  end
end
