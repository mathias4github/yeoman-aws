Vagrant.configure("2") do |config|
  config.vm.box = "mh-aws"

  config.vm.provider :aws do |aws, override|
    override.ssh.username = "admin"
    override.ssh.private_key_path = "~/.ssh/vagrant-test.pem"
    aws.elastic_ip = "52.28.82.97"
  end

  config.vm.provider "vmware_fusion" do |v, override|
    override.vm.box = 'https://s3.eu-central-1.amazonaws.com/ffuenf-vagrantboxes/debian/debian-8.0.0-amd64_vmware.box'
    override.vm.synced_folder './', '/vagrant', type: 'rsync'
  end

  config.vm.define "yeoman-vm" do |machine|

    machine.vm.hostname = "yeoman-vm"

    # Provision the VM using the shell
    config.vm.provision "shell", inline: "apt-get update && apt-get -y install python"

    # Provision the VM using ansible
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "etc/yeoman.yaml"
      config.vm.provider :aws do |ansible|
        ansible.extra_vars = { ansible_ssh_user: 'admin' }
        ansible.skip_tags = "skip_for_aws"
      end
    end
  end
end
