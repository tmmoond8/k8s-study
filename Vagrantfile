# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "m-k8s" do |cfg|
    cfg.vm.box = "sysnet4admin/CentOS-k8s"
    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "m-k8s(github_SysNet4Admin)"
      vb.cpus = 2
      vb.memory = "2048"
      vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
    end
    cfg.vm.host_name = "m-k8s"
    # 책에선192.168.1.10 으로 했지만, https://stackoverflow.com/questions/39049717/vagrant-network-collides-with-a-non-hostonly-network 글을 참조하여 아래 처럼 수정함
    # 나의 경우 51p 의 호스트 전용 네티워크 변경 Tip이 효과가 없었음.
    cfg.vm.network "private_network", ip: "192.168.2.10"
    cfg.vm.network "forwarded_port", guest: 22, host: 60010, auto_correct: true, id: "ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
    cfg.vm.provision "shell", path: "install_pkg.sh" #add proovisioning script
  end  
end
