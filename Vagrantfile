# -*- mode: ruby -*-
# vi: set ft=ruby :

servers = {
  'dojot' => { 'ip' => '10.10.10.10', 'memory' => '4096', 'cpus' => '4' }
}

disk_to_docker = '/tmp/docker.vdi'
disk_to_docker_size = 10

disk_to_k3s = '/tmp/k3s.vdi'
disk_to_k3s_size = 10

Vagrant.configure("2") do |config|

    servers.each do |name, conf|
      config.vm.define "#{name}" do |cfg|
        cfg.vm.box = "ewerton_silva00/ubuntu-minimal-20.04-amd64"
        cfg.vm.box_version = "20220101.0"
        cfg.vm.box_check_update = true
        cfg.vm.hostname = "#{name}.meudominio.local"
        cfg.vm.network "private_network", ip: "#{conf['ip']}"
        cfg.vm.provision :hosts, :sync_hosts => true

        cfg.vbguest.auto_update = false

        cfg.vm.provider "virtualbox" do |vb|
          vb.name = "#{name}"
          vb.gui = false
          vb.cpus = "#{conf['cpus']}"
          vb.memory = "#{conf['memory']}"
          # --- Add second disk with 10GB. Define the variable named 'disk_to_docker'. e.g. 'disk_to_docker' => '/tmp/docker.vdi'
          vb.customize ['createhd', '--filename', disk_to_docker, '--size', disk_to_docker_size * 1024]
          vb.customize ['storageattach', :id, '--storagectl', 'SATA', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk_to_docker]
          # --- Add second disk with 10GB. Define the variable named 'disk_to_k3s'. e.g. 'disk_to_k3s' => '/tmp/k3s.vdi'
          vb.customize ['createhd', '--filename', disk_to_k3s, '--size', disk_to_k3s_size * 1024]
          vb.customize ['storageattach', :id, '--storagectl', 'SATA', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', disk_to_k3s]
        end

        cfg.vm.provision "shell", inline: <<-SHELL
          hostnamectl
        SHELL
      end
    end
end
