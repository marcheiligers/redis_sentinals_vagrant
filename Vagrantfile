# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # ubuntu 64bit image
  config.vm.box = "ubuntu-trusty"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # enable guest auto updates
  unless Vagrant.has_plugin?("vagrant-vbguest")
    raise 'vagrant-vbguest is not installed! run: "vagrant plugin install vagrant-vbguest"'
  end
  config.vbguest.auto_update = true

  config.vm.provider :virtualbox do |vb|
    #vb.gui = true
    # hacky fix for trouble with ipv6 and dns network timeout
    # https://github.com/mitchellh/vagrant/issues/1172
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

  (1..2).each do |i|
    config.vm.define "redis#{i}" do |machine|
      machine.vm.hostname = "redis#{i}"
      machine.vm.network "private_network", ip: "192.168.56.20#{i}"
    end
  end

  (1..3).each do |i|
    config.vm.define "sentinel#{i}" do |machine|
      machine.vm.hostname = "sentinel#{i}"
      machine.vm.network "private_network", ip: "192.168.56.20#{i + 2}"
    end
  end
end
