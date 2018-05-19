Vagrant.require_version ">= 1.5.0"

# update 02.yml if you change this
$USERNAME = 'vagrant'

$SYNC_PATH = '/sync'

$INSTALL_COMMON = <<INSTALL_COMMON
apt-get -q update
apt-get -q install -y zip unzip
INSTALL_COMMON

$INSTALL_DOCKER = <<INSTALL_DOCKER
apt-get -q install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
apt-get -q update
apt-get -q install -y docker-ce
groupmod -aG docker #{$USERNAME}
INSTALL_DOCKER

$INSTALL_VIRTUALBOX = <<INSTALL_VIRTUALBOX
apt-get -q install -y virtualbox
INSTALL_VIRTUALBOX

$PACKER_DEST = "/home/#{$USERNAME}/packer"

$INSTALL_PACKER = <<INSTALL_PACKER
export TMPFILE=`mktemp -q --suffix=zip`
wget --quiet https://releases.hashicorp.com/packer/1.2.3/packer_1.2.3_linux_amd64.zip -O $TMPFILE && unzip -qq $TMPFILE -d $PACKER_DEST && rm $TMPFILE && chmod +x #{$PACKER_DEST}/packer
INSTALL_PACKER

$BOXCUTTER_PATH = "#{$SYNC_PATH}/build/boxcutter"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"

  config.ssh.username = $USERNAME

  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

  config.vm.synced_folder ".", $SYNC_PATH, SharedFoldersEnableSymlinksCreate: true

  config.vm.provision "fix-no-tty", type: "shell" do |s|
    s.privileged = false
    s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  config.vm.provision "shell", inline: $INSTALL_COMMON, name: "Install common", privileged: true
  config.vm.provision "shell", inline: $INSTALL_VIRTUALBOX, name: "Install VirtualBox", privileged: true
  # not necessary for testing
  # config.vm.provision "shell", inline: $INSTALL_DOCKER, name: "Install Docker", privileged: true
  config.vm.provision "shell", inline: $INSTALL_PACKER, name: "Install Packer", privileged: true
end
