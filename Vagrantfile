Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.network "public_network", ip: "192.168.15.157" #ip da maquina local
    config.vm.synced_folder "./docker/", "/docker/"

    config.vm.provision "shell", inline: <<-SHELL
        sudo apt -y remove docker docker-engine docker.io contained runc
        sudp apt update
        sudo apt -y install ca-certificates curl gnupg lsb-release
        sudo mkdir -p /etc/apt/keyrings
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc
        sudo echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        sudo apt update
        sudo apt -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin
        sudo groupadd docker
        sudo usermod -aG docker vagrant
        newgrp docker
    SHELL

    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
    end
end