# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
config.vm.box = "sbeliakou/centos-7.4-x86_64-minimal"
config.ssh.insert_key = false
config.vm.provision "shell", inline: <<-SHELL
yum install -y net-tools telnet htop vim mc zip unzip mlocate git
SHELL
	config.vm.define "jenkins" do |jenkins|
		jenkins.vm.hostname = "jenkins"
		jenkins.vm.network "private_network", ip: "172.22.1.10"
		jenkins.vm.provider "jenkins" do |v|
			v.memory = "2048"
    			v.name = "jenkins"
		end
#<<'COM'
	jenkins.vm.provision "shell", inline: <<-SHELL
		sudo yum install -y java-devel
		wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war -O /opt/jenkins.war
		sudo chown vagrant:vagrant /opt/jenkins.war
		sudo yum install -y nginx
		sudo sed -i '/^        location/a proxy_pass http://127.0.0.1:8080;' /etc/nginx/nginx.conf
		sudo systemctl enable nginx
		sudo systemctl start nginx
		java -jar /opt/jenkins.war
	SHELL
#COM

	end

end







