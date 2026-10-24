Vagrant.configure("2") do |config|
  # Użycie oficjalnego obrazu cloud-image dla Ubuntu 24.04
  config.vm.box = "cloud-image/ubuntu-24.04"
  #
  # Wymuszenie logowania przez SSH na konto "ubuntu" (domyślne dla cloud-image)
  config.ssh.username = "ubuntu"

  # Konfiguracja Cloud-init dla każdej maszyny
  config.vm.cloud_init do |cloud_init|
    cloud_init.content_type = "text/cloud-config"
    cloud_init.inline = <<-EOF
      #cloud-config
      timezone: Europe/Warsaw
      package_update: true
      packages:
        - tmux
        - vim
        - neovim
        - nano
        - mc
    EOF
  end

  # Konfiguracja maszyny: prometheus
  config.vm.define "prometheus" do |node|
    node.vm.hostname = "prometheus"
    node.vm.network :private_network, ip: "192.168.56.10"

    node.vm.provider :libvirt do |v|
      v.cpus = 6
      v.memory = 8096                  # 4 GB RAM
      v.machine_virtual_size = 40      # 40 GB HDD
    end
  end

  # Konfiguracja maszyny: node1
  config.vm.define "node1" do |node|
    node.vm.hostname = "node1"
    node.vm.network :private_network, ip: "192.168.56.11"

    node.vm.provider :libvirt do |v|
      v.cpus = 2
      v.memory = 2048                  # 2 GB RAM
      v.machine_virtual_size = 20      # 20 GB HDD
    end
  end

  # Konfiguracja maszyny: node2
  config.vm.define "node2" do |node|
    node.vm.hostname = "node2"
    node.vm.network :private_network, ip: "192.168.56.12"

    node.vm.provider :libvirt do |v|
      v.cpus = 2
      v.memory = 2048                  # 2 GB RAM
      v.machine_virtual_size = 20      # 20 GB HDD
    end
  end
end
