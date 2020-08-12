  
IMAGE_NAME = "ubuntu/bionic64"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 1
    end
      
    (1..N).each do |i|
        config.vm.define "server-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.99.#{i + 10}"
            node.vm.network "public_network", bridge: "wlp2s0", auto_config: false

            # provision
            node.vm.provision "shell",
                run: "always",
                inline: "ifconfig enp0s9 192.168.1.11 netmask 255.255.255.0 up"

            node.vm.hostname = "server-#{i}"
        end
    end
end