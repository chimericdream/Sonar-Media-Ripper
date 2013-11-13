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

# IP Address
$vm_ip_address    = "66.66.66.10"

$chef_log_level   = :info

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

  # Load the directory containing all the sites
  config.vm.synced_folder $local_music_path, $vm_music_path, :nfs => $nfs_supported

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", $vm_memory]
    vb.customize ["modifyvm", :id, "--cpus",   $vm_cpus]
  end

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled    = true

  config.vm.provision :chef_solo do |chef|
    chef.log_level = $chef_log_level
    chef.add_recipe "abcde"
  end
end