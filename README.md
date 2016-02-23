type: Development

traffic-light: green

target-close-date:

actual-close-date:

affected-group: FEIT

deliverables: Scripts to provision a dev or staging environment for Ozmeka


## AUTO-OZMEKA

A collection of scripts which generate a base Centos 7 "box" file for Vagrant, 
then provision this image into an Ozmeka installation using Vagrant and Ansible.


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

$ ```git clone https://codeine.research.uts.edu.au/eresearch/auto-ozmeka.git```

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


### Generating the base box with Packer

This step isn't necessary for end-users.  Rather, it generates a Centos 7 base 
box which Vagrant will automagically download from https://atlas.hashicorp.com

If you need to build this base box, ensure your Packer installation is up to 
date (http://packer.io) and enter:

$ ```cd auto-ozmeka/packer```

In the atlas.hashicorp admin area, you can create a token to use for uploads.

$ ```packer push -token [insert-your-token-here] -name [your-ac]/c7base template.json```

In roughly half an hour the build should complete.  You can monitor its progress
at https://atlas.hashicorp.com.

Instead of using Atlas, you can also build the box locally with simply

$ ```packer build template.json```

$ ```vagrant box add --name utseresearch/c7base [insert-path-to-local-box-file-here]```

If this went ok, you're ready to run Vagrant.