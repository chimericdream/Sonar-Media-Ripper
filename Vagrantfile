# -*- mode: ruby -*-
# vi: set ft=ruby :

# Basic VM Information
$vm_name          = "sonar-ripper"
$vm_cpus          = "1"
$vm_memory        = "512"
$vm_music_path    = "/vagrantshare/music"

# Host Information
$host_os          = "Win"                      # Assume Windows because fewer things (such as NFS) are supported than on *nix
$nfs_supported    = false
$local_music_path = ENV["HOME"] + "/Music"

# Additional Shared Folders
$shared_folders   = Hash.new

# IP Address & Ports
$vm_ip_address    = "66.66.66.10"
$forwarded_ports  = Hash.new

# Default Proxy Settings
$http_proxy       = nil
$https_proxy      = nil
$noproxy_hosts    = "localhost,127.0.0.1"
$proxy_enabled    = true

$chef_log_level   = :info
$chef_json_extra  = {}

# Override any of the above settings for your local environment
if(File.file?("config.local.rb"))
  require_relative 'config.local.rb'
end

Vagrant.configure("2") do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box      = "precise32"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url  = "http://files.vagrantup.com/precise32.box"

  config.vm.hostname = $vm_name
  config.vm.network :private_network, ip: $vm_ip_address

  $forwarded_ports.each do |host_port, vm_port|
    config.vm.network :forwarded_port, guest: vm_port, host: host_port, auto_correct: true
  end

  # Load the directory where music will be stored
  if(!$host_os.eql?("Win"))
    config.vm.synced_folder $local_music_path, $vm_music_path, :nfs => $nfs_supported

    $shared_folders.each do |host_location, vm_location|
      config.vm.synced_folder host_location, vm_location, :nfs => $nfs_supported
    end
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", $vm_memory]
    vb.customize ["modifyvm", :id, "--cpus",   $vm_cpus]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]

    if($host_os.eql?("Win"))
      vb.customize ["sharedfolder", "add", :id, "--name", "music", "--hostpath", (("//?/" + $local_music_path).gsub("/","\\"))]

      $shared_folders.keys.each_with_index do |host_location, idx|
        vb.customize ["sharedfolder", "add", :id, "--name", "shared_#{idx}", "--hostpath", (("//?/" + host_location).gsub("/","\\"))]
      end
    end
  end

  if($host_os.eql?("Win"))
    config.vm.provision :shell, inline: "mkdir -p #{$vm_music_path}", run: "always"
    config.vm.provision :shell, inline: "mount -t vboxsf -rw -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3` music #{$vm_music_path}", run: "always"

    $shared_folders.values.each_with_index do |vm_location, idx|
      config.vm.provision :shell, inline: "mkdir -p #{vm_location}", run: "always"
      config.vm.provision :shell, inline: "mount -t vboxsf -rw -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3` shared_#{idx} #{vm_location}", run: "always"
    end
  end

  config.omnibus.chef_version = :latest

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = $http_proxy
    config.proxy.https    = $https_proxy
    config.proxy.no_proxy = $noproxy_hosts
    config.proxy.enabled  = $proxy_enabled
  end

  if(File.file?("beforechef.local.sh"))
    config.vm.provision "shell", path: 'beforechef.local.sh'
  end

  config.vm.provision :chef_solo do |chef|
    chef.log_level = $chef_log_level
    chef.json.merge!($chef_json_extra)

    chef.run_list = [
      "recipe[abcde::default]"
    ]
  end

  if(File.file?("provision.local.sh"))
    config.vm.provision "shell", path: 'provision.local.sh'
  end
end