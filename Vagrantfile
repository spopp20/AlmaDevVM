Vagrant.configure("2") do |config|
    config.vm.box = "almalinux/8"
    config.vm.provision "shell", inline: "sudo dnf -y update"
    config.vm.provision "shell", inline: "sudo dnf -y install ansible"
    config.vm.provision "shell", inline: "sudo dnf -y install ansible-core"

    # Prepare for virtualbox guest additions
    config.vm.provision "shell", inline: "sudo dnf -y install gcc make perl kernel-devel kernel-headers bzip2"
    config.vm.provision "shell", inline: "sudo dnf -y update kernel-*"

    # Install xfce and virtualbox 
    config.vm.provision "shell", inline: "sudo dnf -y install epel-release"
    config.vm.provision "shell", inline: "rpm -qi epel-release"
    config.vm.provision "shell", inline: "sudo dnf -y groupinstall 'Xfce' 'base-x'"
    config.vm.provision "shell", inline: "sudo systemctl set-default graphical"
    config.vm.provider :virtualbox do |vb|
        vb.name = "devenv"
        vb.gui = true
        vb.customize [
            "modifyvm", :id,
            "--cpus", "2",                    # CPU: 2core
            "--memory", "10240",              # MEM: 10GB
            "--vram", "256",                  # VRAM: 256 (for full-screen mode)
            "--clipboard", "bidirectional",   # Sharing clipboard
            "--draganddrop", "bidirectional", # Enable drag and drop
            "--ioapic", "on"
        ]
    end
end

