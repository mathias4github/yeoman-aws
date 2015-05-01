Vagrant.configure("2") do |config|
  config.vm.box = "mh-aws"

  config.vm.provider :aws do |aws, override|
    override.ssh.username = "admin"
    override.ssh.private_key_path = "~/.ssh/vagrant-test.pem"
  end

  config.vm.define "yeoman-vm" do |machine|

    machine.vm.hostname = "yeoman-vm"

    # Provision the VM using the shell
    config.vm.provision "shell", inline: "apt-get update && apt-get -y install python"

    # Provision the VM using ansible
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "etc/yeoman.yaml"
      ansible.extra_vars = { ansible_ssh_user: 'admin' }
    end
  end
end