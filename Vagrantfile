# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  # Youtube link: https://www.youtube.com/watch?v=Ib1cyZCiKCs&list=PL8GFhcuc_fW4cxdkRtWIlln1DQ3CZwQen&index=9

  # The following tells vagrant what image we want to use to base our vagrant server on
  config.vm.box = "ubuntu/xenial64"

# The following is a network configuration.
# This forwards the port 8080 on the guest operating system to port 8080 on the host.
# So when we creataing a vagrant box, you're essentially  creating a guest operating system on the host os(this Macbook).
# So our desktop is the host system athat is going to hst a guest image or OS which is going to run the app.
# While developing the app we want to be able to connect to this guest OS by forwarding the port 8080 on the guest to the local host 8080.
# That way we can access any server thts running on port 8080 by going to the local host ip address.

  config.vm.network "forwarded_port", host_ip: "127.0.0.1", guest: 8080, host: 8080

# The following is a provisioning script.
# This runs on the server the first time starting it.
# So when first creating the server, it will run all of the following commands to setup the server to be able to support the application.
  config.vm.provision "shell", inline: <<-SHELL
    # Update and upgrade the server packages.
    sudo apt-get update
    sudo apt-get -y upgrade
    # Set Ubuntu Language
    sudo locale-gen en_GB.UTF-8
    # Install Python, SQLite database and pip
    sudo apt-get install -y python3-dev sqlite python-pip
    # Upgrade pip to the latest version.
    sudo pip install --upgrade pip
    # Install and configure python virtualenvwrapper.

    # The following configures a tool called "virtualenvwrapper"
    # This is a tool that gives shortcut commends that make it easier to work with virtual environments.
    sudo pip install virtualenvwrapper
    if ! grep -q VIRTUALENV_ALREADY_ADDED /home/vagrant/.bashrc; then
        echo "# VIRTUALENV_ALREADY_ADDED" >> /home/vagrant/.bashrc
        echo "WORKON_HOME=~/.virtualenvs" >> /home/vagrant/.bashrc
        echo "PROJECT_HOME=/vagrant" >> /home/vagrant/.bashrc
        echo "source /usr/local/bin/virtualenvwrapper.sh" >> /home/vagrant/.bashrc
    fi
  SHELL

end
