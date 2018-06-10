# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.ssh.insert_key = false    
    config.vm.box = "centos/6"    
    config.vm.network "private_network", ip: "192.168.56.29"

#    config.vm.network "forwarded_port", guest: 22, host: 2223

    config.vm.hostname = "fed.lab.local"

    # Enable Password Auth  
    config.vm.provision "shell", inline: <<-EOC
      sudo sed -i -e "\\#PasswordAuthentication no# s#PasswordAuthentication no#PasswordAuthentication yes#g" /etc/ssh/sshd_config
      sudo service sshd restart
    EOC

    config.vm.provision :ansible do |ansible|
      ansible.playbook = "site.yml"
      # Uncomment next line if you don't want to install Google Authenticator plugin
      #ansible.skip_tags = "totp-authenticator"
    end

    config.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777", "fmode=666"]

end
