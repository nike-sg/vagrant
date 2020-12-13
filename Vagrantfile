$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql -e "CREATE USER 'user1'@'%' IDENTIFIED BY 'user1';" && \
  mysql -e "GRANT ALL PRIVILEGES ON *.* TO 'user1'@'%';" && \
  mysql -e "CREATE DATABASE DB;" && \
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end
  
  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 8080
    mysqlserver.vm.network "private_network", ip: "192.168.50.10"


    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysqlserver"
    end

    mysqlserver.vm.provision "shell", inline: $script_mysql
  end
  
end
