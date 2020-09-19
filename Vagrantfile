NET = "192.168.132"
DOMAIN = ".vntechsol.com"

Vagrant.configure("2") do |config|
  
  vm = 3
  (1..vm).each do |machine_id|
    config.vm.define "redis#{machine_id}" do |machine|
      machine.vm.hostname = "redis#{machine_id}" + DOMAIN
      machine.vm.box = "centos/7"
      machine.vm.network "forwarded_port", guest: 22, host: "229#{machine_id}", id: "ssh"
      machine.ssh.insert_key = false
      machine.vm.network "private_network", ip: NET + ".1#{machine_id}"
      machine.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=755" "fmode=644"]
      machine.vm.boot_timeout = 60

      machine.vm.provider "virtualbox" do |vm|
        vm.cpus = 2
        vm.memory = 2048
        vm.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
      end

      if machine_id = vm
        machine.vm.provision "ansible_local" do |ansible|
          ansible.limit = "all"
          ansible.verbose = true
          ansible.become = true
          ansible.raw_arguments = ["-v"]
          ansible.playbook = "site.yml"
          ansible.tags = ["redis_cluster"]
          ansible.inventory_path = "inventory.ini"
          ansible.extra_vars = {
            ansible_ssh_users: 'vagrant'
          }

          ansible.groups = {
            "redis_node1" => ["redis1"],
            "redis_node2" => ["redis2"], 
            "redis_node3" => ["redis3"]
          }
        end
      end
    end
  end
end
