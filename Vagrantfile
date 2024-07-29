Vagrant.configure("2") do |config|
    config.vm.define "master" do |master|
      # OS
      master.vm.box = "bento/ubuntu-24.04"

      # Networking
      master.vm.hostname = "master.juna"
      master.vm.network :private_network, ip: "10.0.1.10"

      # Disks
      master.vm.disk :disk, size: "100GB", primary: true

      # VirtualBox configuration
      master.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--name", "master"]
        vb.customize ["modifyvm", :id, "--memory", 8192]
        vb.customize ["modifyvm", :id, "--cpus", "4"] 
      end
    end
  
    config.vm.define "worker1" do |worker1|
      # OS
      worker1.vm.box = "bento/ubuntu-24.04"

      # Networking
      worker1.vm.hostname = "worker1.juna"
      worker1.vm.network :private_network, ip: "10.0.1.20"

      # Disks
      worker1.vm.disk :disk, size: "80GB", primary: true  # OS
      
      # VirtualBox configuration
      worker1.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--name", "worker1"]
        vb.customize ["modifyvm", :id, "--memory", 4096]
        vb.customize ["modifyvm", :id, "--cpus", "2"] 
      end
    end

    config.vm.define "worker2" do |worker2|
      # OS
      worker2.vm.box = "bento/ubuntu-24.04"

      # Networking
      worker2.vm.hostname = "worker2.juna"
      worker2.vm.network :private_network, ip: "10.0.1.30"

      # Disks
      worker2.vm.disk :disk, size: "80GB", primary: true

      # VirtualBox configuration
      worker2.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--name", "worker2"]
        vb.customize ["modifyvm", :id, "--memory", 4096]
        vb.customize ["modifyvm", :id, "--cpus", "2"] 
      end
    end
  end