#Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')

$script = <<SCRIPT
  yum -y update
  yum -y install httpd php
  echo '<?php phpinfo(); ?>' > /var/www/html/index.php
  systemctl start httpd
  setenforce 0
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "centos"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.synced_folder "./", "/var/www/html/dev/", type: "sshfs"
  config.vm.provision "shell", inline: $script
end
