# -*- mode: ruby -*-
# # vi: set ft=ruby :

  require 'yaml'
  settings = YAML.load_file(File.join(File.dirname(__FILE__), 'settings.yml'))


Vagrant.configure("2") do |config| 

  config.vm.network "private_network", ip: settings['ip_address']
  config.vm.box = "ubuntu/trusty64"
#  config.vm.box = "scotch/box"
  config.vm.hostname = "mizbox"
    # Use :ansible or :ansible_local to
  # select the provisioner of your choice
  config.vm.provision :ansible do |ansible|
    #ansible.verbose = true
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = {
         ip_address: settings['ip_address'],
         site_path: settings['site_path'],
         site_url: settings['site_url'],
         database_name: settings['database_name'],
         database_username: settings['database_username'],
         database_password: settings['database_password'],
         database_table_prefix: settings['database_table_prefix'],
         wp_site_title: settings['wp_site_title'],
         wp_admin_username: settings['wp_admin_username'],
         wp_admin_password: settings['wp_admin_password'],
         wp_admin_email: settings['wp_admin_email']
      }
    # ansible.sudo = true
    # ansible.sudo_user = 'vagrant'
    ansible.inventory_path = "vagrant-inventory"

    #ansible.host_key_checking = "false"
    ansible.limit = "all"
  end
  config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
end