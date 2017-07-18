Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  # config.ssh.username = "developer"
  # config.ssh.password = "Abcd123!"

  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.name = "devmachine"
    v.memory = 4000
    v.cpus = 2
    #v.customize ["storagectl", :id, "--name", "IDEController", "--add", "ide"]
    v.customize ["storageattach", :id, "--storagectl", "IDE Controller", "--port", "0", "--device", "0", "--type", "dvddrive", "--medium", "emptydrive"]
    v.customize ["modifyvm", :id, "--boot1", "disk", "--boot2", "dvd"]
    v.customize ["modifyvm", :id, "--vram", "32"]
  end

  config.vm.hostname = "devmachine"
  config.vm.network :private_network, ip: "192.168.30.30"

  config.vm.define :devmachine do |devmachine|
  end

  # Run Ansible from the Vagrant VM
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = 'hosts'
    ansible.verbose = true
    ansible.install = true
    ansible.limit = "all"
    ansible.inventory_path = "inventory"
    #ansible.sudo = true
  end

end
