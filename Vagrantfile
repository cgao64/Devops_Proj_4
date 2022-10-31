Vagrant.configure("2") do |config|
  servers=[
      {
        :hostname => "jenkins-server",
        :box => "bento/ubuntu-22.04",
        :ip => "192.168.202.50",
        :ssh_port => '2200'
      },
      {
        :hostname => "webapp-server",
        :box => "bento/ubuntu-22.04",
        :ip => "192.168.202.52",
        :ssh_port => '2202'
      },

    ]

  servers.each do |machine|
      config.vm.define machine[:hostname] do |node|
          node.vm.box = machine[:box]
          node.vm.hostname = machine[:hostname]
          node.vm.network :private_network, ip: machine[:ip]
          node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
          node.vm.provider :virtualbox do |vb|
              vb.customize ["modifyvm", :id, "--memory", 512]
              vb.customize ["modifyvm", :id, "--cpus", 1]
          end
      end
  end
end