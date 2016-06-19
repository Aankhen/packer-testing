Vagrant.require_version ">= 1.5.0"

# update 02.yml if you change this
$USERNAME = 'vagrant'

$SYNC_PATH = '/sync'

$BOOTSTRAP_ANSIBLE = <<BOOTSTRAP_ANSIBLE
apt-get update -y
apt-get install -y g++ python-pip python-dev libssl-dev libffi-dev build-essential libyaml-dev
pip install ansible
BOOTSTRAP_ANSIBLE

# Ansible 2.2+ will have a systemd module
$DOCKER_SYSTEMD = <<DOCKER_SYSTEMD
systemctl enable docker
systemctl restart docker
DOCKER_SYSTEMD

$BOXCUTTER_PATH = "#{$SYNC_PATH}/build/boxcutter"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/wily64"

  config.ssh.username = $USERNAME

  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
  end

  config.vm.synced_folder ".", $SYNC_PATH

  config.vm.provision "fix-no-tty", type: "shell" do |s|
    s.privileged = false
    s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  config.vm.provision "shell", inline: $BOOTSTRAP_ANSIBLE, name: "apt", privileged: true

  config.vm.provision "file", source: "playbooks", destination: "/tmp/playbooks"

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "01.yml"
    ansible.install = false
    ansible.provisioning_path = "/tmp/playbooks"
  end

  config.vm.provision :reload, name: "Reboot"

  # rebooting seems to wipe out /tmp/playbooks
  config.vm.provision "file", source: "playbooks", destination: "/tmp/playbooks"

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "02.yml"
    ansible.install = false
    ansible.provisioning_path = "/tmp/playbooks"
  end

  config.vm.provision "shell", inline: $DOCKER_SYSTEMD, name: "Docker systemd config", privileged: true
end