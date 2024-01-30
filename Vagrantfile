Vagrant.configure("2") do |zabbix|
   zabbix.vm.box = "bento/ubuntu-22.04"
  
   zabbix.vm.provider "virtualbox" do |i|
    i.name = "zabbix"
    i.memory = "4096"
    i.cpus = 2
   end
   zabbix.vm.hostname = "zabbix"
   zabbix.vm.network "forwarded_port", guest: 8080 , host: 8080, host_ip: "127.0.0.1"
   zabbix.vm.network "forwarded_port", guest: 5432 , host: 5432, host_ip: "127.0.0.1"
   zabbix.vm.network "forwarded_port", guest: 10050 , host: 10050, host_ip: "127.0.0.1"
   zabbix.vm.network "forwarded_port", guest: 10051 , host: 10051, host_ip: "127.0.0.1"
   zabbix.vm.provision :file, source: 'docker-compose.yaml', destination: '/home/vagrant/'
   zabbix.vm.provision "shell", inline: <<-SHELL
            # Add Docker's official GPG key:
            sudo apt-get update
            sudo apt-get install -y ca-certificates curl gnupg
            sudo install -m 0755 -d /etc/apt/keyrings
            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
            sudo chmod a+r /etc/apt/keyrings/docker.gpg
            # Add the repository to Apt sources:
            echo \
            "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
            $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
            sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
            sudo apt-get update
            apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose zabbix-agent
            sudo docker-compose up -d
            sudo sed -i.bak 's/ServerActive=127.0.0.1/ServerActive=172.28.0.254/g' /etc/zabbix/zabbix_agentd.conf
            sudo sed -i.bak 's/Server=127.0.0.1/Server=172.28.0.254/g' /etc/zabbix/zabbix_agentd.conf
            sudo systemctl restart zabbix-agent
        SHELL
  zabbix.vm.synced_folder '.', '/vagrant', disabled: true
  end