Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"  

  # Loop to create 4 VMs
  (1..4).each do |i|
    config.vm.define "ubuntu_vm_#{i}" do |vm|
      # Set a static IP for each VM from 192.168.1.21
      vm.vm.network "private_network", ip: "192.168.1.#{20 + i}"

      # Configure VirtualBox as the provider
      vm.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntu_vm_#{i}"  # Set Name of the VM
        vb.memory = "512"           # Set RAM for the VM
        vb.cpus = 1                 # Set CPU count
      end

      # Ensure the VM has internet access by using a bridged network interface
      vm.vm.network "public_network", bridge: "wlp0s20f3", auto_config: true
    end
  end

  # Ansible provisioner
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/run_vagrant_provision.yml" 
    ansible.compatibility_mode = "2.0"
    ansible.extra_vars = {
      ansible_python_interpreter: "/usr/bin/python3"
    }
  end
end
