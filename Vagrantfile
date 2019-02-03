# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "standard", primary: true do |machine|
    machine.vm.provider "docker" do |d|
      d.image      = "emmadxj/ubuntu-trusty-vagrantbox"
      d.has_ssh    = true
    end
    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/deploy.yml"
    end
    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/test.yml"
    end
  end
  config.vm.define "docker-build-image", autostart: false do |machine|
    machine.vm.provider "docker" do |d|
      d.image      = "emmadxj/vagrantbox-docker"
      d.has_ssh    = true
      d.privileged = true
    end
    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/deploy.yml"
    end
    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/test.yml"
    end
  end
  config.vm.define "docker-pull-image", autostart: false do |machine|
    machine.vm.provider "docker" do |d|
      d.image      = "emmadxj/vagrantbox-docker"
      d.has_ssh    = true
      d.privileged = true
    end
    machine.vm.provision "ansible" do |ansible|
      ansible.extra_vars = {
        mariadb_docker_username: "emmadxj",
        mariadb_docker_build_image: false
      }
      ansible.playbook = "provisioning/deploy.yml"
    end
    machine.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/test.yml"
    end
  end
end

