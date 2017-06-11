require_relative './vagrant/key_authorization'

$update_apt_sources = <<-EOL
echo -e "deb [arch=amd64] http://192.168.33.1:9999/ubuntu xenial main restricted universe multiverse
deb [arch=amd64] http://192.168.33.1:9999/ubuntu xenial-updates main restricted universe multiverse
deb [arch=amd64] http://192.168.33.1:9999/ubuntu xenial-security main restricted universe multiverse" > /etc/apt/sources.list
EOL

Vagrant.configure('2') do |config|
  authorize_key_for_root config, '~/.ssh/id_rsa.pub'
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = false

  {
    'ubuntu-xenial'   => '192.168.33.10',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.box = 'bento/ubuntu-16.04'
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}.vagrant"
      host.hostmanager.aliases = "#{short_name}"
      host.vm.provision 'shell', inline: $update_apt_sources
    end
  end

  {
    'centos-7'   => '192.168.33.20',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.box = 'centos/7'
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}.vagrant"
      host.hostmanager.aliases = "#{short_name}"
    end
  end
end
