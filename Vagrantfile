Vagrant.configure("2") do |config|
  
  # Define base box
  config.vm.box = "ubuntu/jammy64"  

  # Define an array of VM configurations
  vms = [
    { name: "db1", ip: "192.168.1.21" },
    { name: "db2", ip: "192.168.1.22" },
    { name: "db3", ip: "192.168.1.23" },
    { name: "router", ip: "192.168.1.100" }
  ]

  # Loop to create each VM based on the configuration
  vms.each do |vminfo|
    config.vm.define vminfo[:name] do |vm|

      # Set hostname for each the VM
      vm.vm.hostname = vminfo[:name]

      # Configure VirtualBox as the provider
      vm.vm.provider "virtualbox" do |vb|
        vb.name = vminfo[:name]     # Set Name of the VM
        vb.memory = "512"           # Set RAM for the VM
        vb.cpus = 1                 # Set CPU count
      end

      # Ensure the VM has internet access by using a bridged network interface
      vm.vm.network "public_network", bridge: "wlp0s20f3", auto_config: true
      # Set a static IP for each VM from 192.168.1.21
      vm.vm.network "private_network", ip: vminfo[:ip]
    
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
