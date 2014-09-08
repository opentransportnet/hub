# -*- mode: ruby -*-
# vi: set ft=ruby :

tdt_ip                   = "192.168.70.70"
tdt_hostname             = "tdt.hub.dev"
db_ip                    = "192.168.70.71"

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
require 'rbconfig'
WINDOWS = (RbConfig::CONFIG['host_os'] =~ /mswin|mingw|cygwin/) ? true : false

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # please see the online documentation at vagrantup.com


  # This is the machine containing the databases
  config.vm.define "db" do |db|
    db.vm.box = "precise64"
    db.vm.box_url = "http://files.vagrantup.com/precise64.box"
    db.vm.network :private_network, ip: db_ip
    db.vm.hostname = "db"
    
    # chef solo configuration
    db.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "./"
      # chef debug level, start vagrant like this to debug:
      # $ CHEF_LOG_LEVEL=debug vagrant <provision or up>
      chef.log_level = ENV['CHEF_LOG'] || "info"
      
      # chef recipes/roles
      chef.add_recipe("vagrant-db")
      
      host_ip = db_ip[/(.*\.)\d+$/, 1] + "1"
      
      chef.json = {
        :host_ip => host_ip,
        :xdebug_enabled => true,
        :xdebug_remote_enable => "1",
        :xdebug_remote_port => "9000",
        :xdebug_profiler_output_dir => "/vagrant/xdebug",
        :xdebug_trace_output_dir => "/vagrant/xdebug"
      }
    end
  end


  
  # This is the machine container a The DataTank installation
  config.vm.define "tdt" do |tdt|
    # Use ubuntu 14.04 64 bit
    tdt.vm.box = "precise64"
    tdt.vm.box_url = "http://files.vagrantup.com/precise64.box"
    tdt.vm.synced_folder ".", "/vagrant", :nfs => !WINDOWS
    tdt.vm.network :private_network, ip: tdt_ip
    tdt.vm.hostname = tdt_hostname

    # chef solo configuration
    tdt.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "./"
      # chef debug level, start vagrant like this to debug:
      # $ CHEF_LOG_LEVEL=debug vagrant <provision or up>
      chef.log_level = ENV['CHEF_LOG'] || "info"
      
      # chef recipes/roles
      chef.add_recipe("vagrant-tdt")
      
      host_ip = tdt_ip[/(.*\.)\d+$/, 1] + "1"
      
      chef.json = {
        :host_ip => host_ip,
        :host_name => tdt_hostname,
        :xdebug_enabled => true,
        :xdebug_remote_enable => "1",
        :xdebug_remote_port => "9000",
        :xdebug_profiler_output_dir => "/vagrant/xdebug",
        :xdebug_trace_output_dir => "/vagrant/xdebug"
      }
    end

  end


end
