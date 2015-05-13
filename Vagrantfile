domain = 'test.local'

nodes = [
  { :hostname => 'test1',  :ip => '192.168.0.2', :box => 'wheezy64_with_puppet', :ram => 1024 },
  { :hostname => 'test2',  :ip => '192.168.0.3', :box => 'wheezy64_with_puppet', :ram => 1024 }
]

Vagrant::Config.run do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.box = node[:box]
      node_config.vm.host_name = node[:hostname] + '.' + domain
      node_config.vm.network :hostonly, node[:ip]

      memory = node[:ram] ? node[:ram] : 1024;
      node_config.vm.customize [
        'modifyvm', :id,
        '--name', node[:hostname],
        '--memory', memory.to_s
      ]
    end
  end

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = 'puppet/manifests'
    puppet.manifest_file = 'site.pp'
    puppet.module_path = 'puppet/modules'
  end
end
