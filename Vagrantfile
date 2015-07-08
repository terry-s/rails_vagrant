# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Наша операційна система буде Ubuntu 14.04 Trusty Tahr 64-bit
  config.vm.box = "ubuntu/trusty64"

  # Налаштовуємо VirtualBox на використання нашою
  # операційною системою 1GB оперативної пам'яті.
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus   = 2
    # vb.gui    = true
  end

  # Призначаємо стандартні порти для Rails та нашої хост системи
  config.vm.network :forwarded_port, guest: 3000, host: 3000

  # Використовуємо Chef Solo, аби налаштувати нашу віртуальну систему
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]

    # Налаштування кожного cookbooks можна знайти на сайті
    # supermarket.chef.io скориставшись пошуком
    chef.add_recipe "apt"
    chef.add_recipe "build-essential::default"
    chef.add_recipe "ruby_build"
    chef.add_recipe "nodejs"
    chef.add_recipe "vim"
    chef.add_recipe "git"
    chef.add_recipe "chef_rvm::default"
    chef.add_recipe "zshell::default"
    chef.add_recipe "oh_my_zsh"

    # chef.add_recipe "postgresql"
    # chef.add_recipe "mysql::server"
    # chef.add_recipe "mysql::client"
    # chef.add_recipe "rbenv::user"
    # chef.add_recipe "rbenv::vagrant"

    chef.json = {
      chef_rvm: {
        rvmrc: {
          'rvm_gem_options' => '--no-rdoc --no-ri',
          'rvm_autoupdate_flag' => 0
        },
        users: {
          vagrant: {
            rubies: {
              '2.2.2' => 'install',
            }
          }
        }
      },
      oh_my_zsh: {
        users: [
          {
            login: 'vagrant',
            theme: 'agnoster',
            plugins: ['gem', 'git', 'ruby']
          }
        ]
      }
    }
  end
end
