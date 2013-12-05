# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_NAME = ENV["BOX_NAME"] || "raring"
BOX_URI = ENV["BOX_URI"] || "https://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-amd64-vagrant-disk1.box"
CBC_DOMAIN = ENV["CBC_DOMAIN"] || "localtest.me"
CBC_IP = ENV["CBC_IP"] || "10.0.0.3"

Vagrant::configure("2") do |config|
  config.vm.box = BOX_NAME
  config.vm.box_url = BOX_URI
  config.vm.network :forwarded_port, guest: 80, host: 9000
  config.vm.hostname = "#{CBC_DOMAIN}"
  config.vm.network :private_network, ip: CBC_IP

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # Ubuntu's Raring 64-bit cloud image is set to a 32-bit Ubuntu OS type by
    # default in Virtualbox and thus will not boot. Manually override that.
    vb.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
  end

  config.vm.provision :shell, :inline => "/vagrant/stack/prepare #{CBC_DOMAIN}"

end
