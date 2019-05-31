# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

required_plugins = %w( vagrant-hostsupdater vagrant-berkshelf vagrant-omnibus )
required_plugins.each do |plugin|
  exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end


Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
     app.vm.box = "ubuntu/xenial64"
     app.vm.network "private_network", ip: "192.168.10.100"
     app.hostsupdater.aliases = ["localhost"]
     app.vm.synced_folder "app", "/home/ubuntu/app"
     app.vm.provision "chef_solo" do |chef|
       chef.add_recipe "nginx_proxy::default"
       chef.add_recipe "snu_python::default"
       chef.version = "14.12.9"
     end
     # app.vm.provision "shell", inline: set_env({ DB_HOST: "mongodb://192.168.10.150:27017/posts"}), privileged: false
   end
end
