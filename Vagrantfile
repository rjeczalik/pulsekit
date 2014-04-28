# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$provision = <<SCRIPT
	sudo apt-get update
	sudo apt-get install -y python-software-properties
	echo | sudo add-apt-repository ppa:webupd8team/java
	sudo apt-get update
	echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
	sudo apt-get install -y oracle-java7-installer git
	wget http://zutubi.com/download/pulse-2.6.19.tar.gz
	tar xf pulse-2.6.19.tar.gz
	ln -s pulse{-2.6.19,}
	echo JAVA_HOME=/usr/lib/jvm/java-7-oracle | sudo tee -a /etc/environment
	echo PULSE_HOME=/home/vagrant/pulse | sudo tee -a /etc/environment
	source /etc/environment
	sudo ln -s $PULSE_HOME/bin/init.sh /etc/init.d/pulse
	# sed -i -e 's:#RUN_AS_USER=:RUN_AS_USER=vagrant:' $PULSE_HOME/bin/init.sh
	sudo update-rc.d pulse defaults
	sudo update-rc.d pulse enable
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.provision :shell, :inline => $provision
end
