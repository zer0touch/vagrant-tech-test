# This env is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"

Vagrant.configure(2) do |config|

  config.vm.box = "bento/ubuntu-16.04"

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false
  config.hostmanager.enabled = true

  # Update host machine's /etc/hosts
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true

  # Don't ignore private IPs
  config.hostmanager.ignore_private_ip = false

  # Include offline VMs (rather than just active ones)
  config.hostmanager.include_offline = true

  # Bring up the primary build box
  config.vm.define "build", primary: true do |build|
    build.vm.provider "virtualbox" do |vb, override|
      vb.memory = "4096"
      vb.cpus = "2"
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
    
    # Port forward sonar, jenkins and selenoid
    build.vm.network :forwarded_port, guest: 9000, host: 9091
    build.vm.network :forwarded_port, guest: 8080, host: 8081
    build.vm.network :private_network, ip: "10.0.0.10"
  
    build.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "ansible/build.yml"
      ansible.vault_password_file = ".vault_pass.txt"
    end
  end

  # Bring up the target build box
  config.vm.define "target", primary: false do |target|
    target.vm.provider "virtualbox" do |vb, override|
      vb.memory = "1500"
      vb.cpus = "1"
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
    
    # Port-forward our application port
    target.vm.network :forwarded_port, guest: 8080, host: 8082
    target.vm.network :private_network, ip: "10.0.0.11"
    
    # Run ansible on our guest
    target.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      #ansible.playbook = "ansible/target.yml"
      ansible.playbook = "ansible/build.yml"
      ansible.tags = "base"
      ansible.vault_password_file = ".vault_pass.txt"
    end
  end
end


