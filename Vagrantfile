Vagrant.configure("2") do |config|
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 1
  end

  config.vm.define "dc" do |dc|
    dc.vm.guest = :windows
    dc.vm.communicator = "winrm"
    dc.vm.boot_timeout = 600
    dc.vm.graceful_halt_timeout = 600
    dc.winrm.retry_limit = 30
    dc.winrm.retry_delay = 10
    dc.vm.box = "StefanScherer/windows_2019"
    dc.vm.network "private_network", ip: "192.168.56.10"
    dc.vm.network :forwarded_port, guest: 3389, host: 23389, id: "msrdp"
    dc.vm.network :forwarded_port, guest: 5985, host: 25985, id: "winrm"
    dc.vm.provision "shell", path:"scripts/ConfigureRemotingForAnsible.ps1"
  end

  config.vm.define "win_server" do |win_server|
    win_server.vm.guest = :windows
    win_server.vm.communicator = "winrm"
    win_server.vm.boot_timeout = 600
    win_server.vm.graceful_halt_timeout = 600
    win_server.winrm.retry_limit = 30
    win_server.winrm.retry_delay = 10
    win_server.vm.box = "StefanScherer/windows_2019"
    win_server.vm.network "private_network", ip: "192.168.56.11"
    win_server.vm.network :forwarded_port, guest: 3389, host: 33389, id: "msrdp"
    win_server.vm.network :forwarded_port, guest: 5985, host: 35985, id: "winrm"
    win_server.vm.provision "shell", path:"scripts/ConfigureRemotingForAnsible.ps1"
  end

  config.vm.define "win_workstation" do |win_workstation|
    win_workstation.vm.guest = :windows
    win_workstation.vm.communicator = "winrm"
    win_workstation.vm.boot_timeout = 600
    win_workstation.vm.graceful_halt_timeout = 600
    win_workstation.winrm.retry_limit = 30
    win_workstation.winrm.retry_delay = 10
    win_workstation.vm.box = "StefanScherer/windows_10"
    win_workstation.vm.network "private_network", ip: "192.168.56.12"
    win_workstation.vm.network :forwarded_port, guest: 3389, host: 43389, id: "msrdp"
    win_workstation.vm.network :forwarded_port, guest: 5985, host: 45985, id: "winrm"
    win_workstation.vm.provision "shell", path:"scripts/ConfigureRemotingForAnsible.ps1"
  end

  config.vm.define "ubuntu_domain" do |ubuntu_domain|
    ubuntu_domain.vm.box = "ubuntu/focal64"
    ubuntu_domain.vm.network "private_network", ip: "192.168.56.13"
    ubuntu_domain.vm.network :forwarded_port, guest: 22, host: 10022, id: "msrdp"

    ubuntu_domain.vm.provision "shell" do |s|
      ssh_prv_key = ""
      ssh_pub_key = ""
      if File.file?("#{Dir.home}/.ssh/id_ed25519")
        ssh_prv_key = File.read("#{Dir.home}/.ssh/id_ed25519")
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_ed25519.pub").first.strip
      else
        puts "No SSH key found. You will need to remedy this before pushing to the repository."
      end
      s.inline = <<-SHELL
        if grep -sq "#{ssh_pub_key}" /home/vagrant/.ssh/authorized_keys; then
          echo "SSH keys already provisioned."
          exit 0;
        fi
        echo "SSH key provisioning."
        mkdir -p /home/vagrant/.ssh/
        touch /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} > /home/vagrant/.ssh/id_rsa.pub
        chmod 644 /home/vagrant/.ssh/id_rsa.pub
        echo "#{ssh_prv_key}" > /home/vagrant/.ssh/id_rsa
        chmod 600 /home/vagrant/.ssh/id_rsa
        chown -R vagrant:vagrant /home/vagrant
        exit 0
      SHELL
    end
  end

  config.vm.define "ubuntu_outside" do |ubuntu_outside|
    ubuntu_outside.vm.box = "ubuntu/focal64"
    ubuntu_outside.vm.network "private_network", ip: "192.168.56.14"
    ubuntu_outside.vm.network :forwarded_port, guest: 22, host: 20022, id: "msrdp"
    ubuntu_outside.vm.provision "shell" do |s|
      ssh_prv_key = ""
      ssh_pub_key = ""
      if File.file?("#{Dir.home}/.ssh/id_ed25519")
        ssh_prv_key = File.read("#{Dir.home}/.ssh/id_ed25519")
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_ed25519.pub").first.strip
      else
        puts "No SSH key found. You will need to remedy this before pushing to the repository."
      end
      s.inline = <<-SHELL
        if grep -sq "#{ssh_pub_key}" /home/vagrant/.ssh/authorized_keys; then
          echo "SSH keys already provisioned."
          exit 0;
        fi
        echo "SSH key provisioning."
        mkdir -p /home/vagrant/.ssh/
        touch /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        echo #{ssh_pub_key} > /home/vagrant/.ssh/id_rsa.pub
        chmod 644 /home/vagrant/.ssh/id_rsa.pub
        echo "#{ssh_prv_key}" > /home/vagrant/.ssh/id_rsa
        chmod 600 /home/vagrant/.ssh/id_rsa
        chown -R vagrant:vagrant /home/vagrant
        exit 0
      SHELL
    end
  end

end
