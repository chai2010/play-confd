# Copyright 2017 <chaishushan{AT}gmail.com>. All rights reserved.
# Use of this source code is governed by a Apache
# license that can be found in the LICENSE file.

# vagrant up
# vagrant reload
# vagrant status
# vagrant ssh

# vagrant halt
# vagrant destroy

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false

  config.vm.synced_folder "./v-root", "/vagrant"
  config.vm.network "forwarded_port", guest: 80, host: 8081

  config.vm.provision "shell", path: "bootstrap.sh"
  config.vm.provision "shell", inline: <<-SHELL
    echo "done"
  SHELL
end
