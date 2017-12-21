# Copyright 2017 <chaishushan{AT}gmail.com>. All rights reserved.
# Use of this source code is governed by a Apache
# license that can be found in the LICENSE file.

# vagrant up
# vagrant reload
# vagrant status
# vagrant ssh

# vagrant halt
# vagrant destroy

# vagrant reload --provision
# vagrant reload --provision-with shell

Vagrant.configure(2) do |config|
  # https://github.com/tmatilai/vagrant-proxyconf
  # vagrant plugin install vagrant-proxyconf
  if Vagrant.has_plugin?("vagrant-proxyconf")
    #config.proxy.http     = "http://127.0.0.1:2081/"
    #config.proxy.https    = "http://127.0.0.1:2081/"
    #config.proxy.no_proxy = "localhost,127.0.0.1,.example.com"
  end

  config.vm.box = "centos/7"
  config.vm.box_check_update = false

  config.vm.synced_folder "./v-root", "/vagrant"
  config.vm.network "forwarded_port", guest: 80, host: 8081

  # https://www.vagrantup.com/docs/provisioning/basic_usage.html
  config.vm.provision "shell", path: "bootstrap.sh"
  config.vm.provision "shell", inline: <<-SHELL
    uname -a
    lsb_release -a

    # install docker
    # https://docs.docker.com/engine/installation/linux/docker-ce/centos/#set-up-the-repository

    sudo yum remove docker docker-common docker-selinux docker-engine
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    sudo yum install -y docker-ce
    sudo systemctl start docker
    sudo docker run hello-world

    echo "done"
  SHELL
end
