VAGRANTFILE_API_VERSION ||= "2"

box = "ubuntu/trusty64"
name = "vagrant-ansible-mean"
ipaddr = "192.168.0.30"
playbook = "ansible/mean.yml"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box_check_update = false

	config.vm.define name, primary: true do |app|
		app.vm.box = box
		app.vm.network :private_network, ip: ipaddr
		app.vm.provider :virtualbox do |vb|
			vb.name = name
		end
		app.vm.provision :ansible_local do |ansible|
			ansible.playbook = playbook
		end
#		app.vm.synced_folder ".", "/vagrant", type: "nfs"
#		app.vm.synced_folder ".", "/vagrant", type: "rsync", owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
#		app.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]

	end
end
