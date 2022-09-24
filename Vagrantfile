VAGRANTFILE_API_VERSION = "2"
OFFSET = 10

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # hosts resolver
  config.vm.provision :hosts do |resolver|
    resolver.add_host "192.168.56.#{OFFSET}", ["master"]
    (1..2).each do |i|
      resolver.add_host "192.168.56.#{OFFSET+i}", ["worker-#{i}"]
    end
  end

  # master
  config.vm.define "master" do |master|
  master.vm.box = "generic/ubuntu2204"
  master.vm.hostname = "master"
  master.vm.network :private_network, ip: "192.168.56.#{OFFSET}"
  master.vm.provision :hosts, :sync_hosts => true
  end

  # worker
  (1..2).each do |i|
    config.vm.define "worker-#{i}" do |worker|
    worker.vm.box = "generic/ubuntu2204"
    worker.vm.hostname = "worker-#{i}"
    worker.vm.network :private_network, ip: "192.168.56.#{OFFSET+i}"
    worker.vm.provision :hosts, :sync_hosts => true
    end
  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
