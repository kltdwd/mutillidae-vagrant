# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/focal64"

  config.vm.network "private_network", type: "dhcp"

  config.vm.provision "shell", inline: <<-SHELL
      echo "mysql-server mysql-server/root_password password mutillidae" | debconf-set-selections
      echo "mysql-server mysql-server/root_password_again password mutillidae" | debconf-set-selections
      apt update -y
      apt install apache2 libapache2-mod-php mysql-server php-mysql php-curl php-mbstring php-xml -y
      systemctl enable mysql
      systemctl enable apache2
      rm -Rf /var/www/html
      git clone https://github.com/webpwnized/mutillidae.git /var/www/html 2>&1 1>/dev/null
      curl http://localhost/set-up-database.php
      
 SHELL

end
