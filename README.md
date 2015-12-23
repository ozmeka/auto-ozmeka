## AUTO-OZMEKA

A collection of scripts which uses a base Centos 7 "box" file for Vagrant, 
then provisions an Ozmeka installation using Vagrant and Ansible.


### Who is this for?

People and organisations who want to make a rich collection of linked data 
accessible via the world-wide web.  Particularly those who would like to have
canonical URIs for item data such as places, subjects and so on.


### Prerequisites:  

You'll need the following software installed on your local system:

- Git - http://git-scm.com/downloads
- Virtualbox - http://www.virtualbox.org/
- Vagrant - http://vagrantup.com/
- Ansible - http://www.ansible.com/


#### Installing Ansible

Installation instructions for Ansible can be found at 
http://docs.ansible.com/ansible/intro_installation.html and official packages 
are available for many Linux and UNIX flavours.

For OSX see 
http://docs.ansible.com/ansible/intro_installation.html#latest-releases-on-mac-osx 
which basically boils down to opening Terminal and entering:

$ ```sudo easy_install pip```

Then for OSX 10.9 and earlier: 

$ ```sudo pip install ansible```

Or for OSX 10.10 (Mavericks): 

$ ```sudo CFLAGS=-Qunused-arguments CPPFLAGS=-Qunused-arguments pip install ansible```

Vagrant requires the vagrant-vbguest plugin; it will install this by itself.


### Now clone the Ozmeka scripts:

$ ```git clone https://github.com/ozmeka/auto-ozmeka.git```

$ ```cd auto-ozmeka/vagrant```

You can review configuration options and alter them if necessary in the 
provisioning/group_vars/config.yml file.


### Launch the VM

$ ```vagrant up```

This will start the provisioner, which will automatically download a Centos 7 
base box for Vagrant.  After that, it will install Ozmeka automatically, which 
typically takes 5-10 minutes.

Once the provisioning script has completed, point your browser 
at http://localhost:8080/install/install.php and set up Omeka.  Don't forget to 
enable the plugins and theme in the admin section once you've finished initial 
setup.

To shut down the VM when you're finished, use $ ```vagrant halt```.  You can 
also use $ ```vagrant suspend``` to pause it.  If you made an awful mess of it 
and want to start again from scratch, $ ```vagrant destroy``` will give you a 
blank slate.  To bring the VM back up in all these cases, simply issue 
$ ```vagrant up```.

