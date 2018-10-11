Vagrant.configure("2") do |config|

  config.ssh.insert_key = false
  config.vbguest.auto_update = false

  if Vagrant.has_plugin?("vagrant-vbguest") then
    # Guest Additions自動更新の無効化設定
    config.vbguest.auto_update = false
  end

  config.vm.box = "bento/centos-7.3"

  # 共有フォルダの設定
  config.vm.synced_folder ".", "/vagrant",  create: true, owner: "vagrant", group: "vagrant"

  config.vm.define "tks-front" do |server|
    server.vm.hostname = "tks-front"
    server.vm.network :private_network, ip: "192.168.33.10"

    # VirtualBoxのGUI上の名前を設定する
    server.vm.provider "virtualbox" do |vb|
      vb.name = config.vm.box.gsub(/\//, "_") + "_" + server.vm.hostname
    end

    server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "docker.yml"
    end

  end
end
