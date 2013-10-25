Getting MEAN with Vagrant and Ansible
=====================================

This is half a lie because you will likely want to install Express (the "E" in MEAN) on a project by project basis. Other than that - everything else is good to go.

Installation
------------
Install [Vagrant 1.3.5](http://downloads.vagrantup.com/)
Install [VirtualBox 4.3](https://www.virtualbox.org/wiki/Downloads)
Install [Ansible](http://www.ansibleworks.com/docs/intro_installation.html)

Running
-------
Running and provisioning can be handled nicely:

```
vagrant up --provision
```

You can SSH into the provisioned vm like so:

```
vagrant ssh
```

And stop it:

```
vagrant halt
```

Voila! You have a development enviroment with the latest and greatest Node.js, MongoDB, and Yeoman.

Note: part of the provisioning process ensures that Mongo is already running on it's default port.

Ansible
-------
Ansible is configured to run for the vagrant host and you can see the specified private IP in `provisioning/hosts`. 

If for some reason you want to use a different IP, be aware that you will need to update the `Vagrantfile` as well as `provisioning/hosts`.

```ruby
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.111.222"
end
```

Ansible installs the following packages:
*git
*nodejs
*mongodb
*yeoman
*generator-angular for yeoman

And the mongodb service is started after provisioning takes place.

Synced Folders
--------------
By default this repo disables directory syncing. If you wish to have this environment checked in as part of the dev process you can create your source directory in the top level of the project and uncomment this line in the `Vagrantfile`:

```ruby
# config.vm.synced_folder "src/", "/home/vagrant/path/to/your/project"
```

This will sync your source folders over SSH so you can develop on your host machine.
