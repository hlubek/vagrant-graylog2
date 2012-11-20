# Launch graylog2 in a VM with a single command
# vagrantup.com

Vagrant::Config.run do |config|
  config.vm.box = "lucid64"

  # Forward the vm's port 80 to your 8080
  config.vm.forward_port 80, 8080
  config.vm.forward_port 443, 4433

  # Forward GELF port with UDP
  config.vm.forward_port 12201, 12201, {:protocol => "udp"}

  # Forward elasticsearch-head
  config.vm.forward_port 9200, 9201

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "graylog2"

    # Specify chef attributes
    # chef.json.merge!({
    #   :graylog2 => {
    #     :send_stream_subscriptions => false
    #   }
    # })
  end

  config.vm.customize ["modifyvm", :id, "--memory", 1024]
end
