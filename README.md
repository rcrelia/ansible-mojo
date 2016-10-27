# ansible-mojo

## Description

A simple introductory demo of Ansible playbook operations.

For more in-depth discussion, check out this [blog post](https://randops.org/2016/10/26/ansible-shenanigans-part-i/).

## Installation

* Clone this repo down to the system you'll be running Ansible from and make it your working directory
  * `$ cd $HOME/code`
  * `$ git clone https://github.com/rcrelia/ansible-mojo.git`
  * `$ cd ansible-mojo`
* Create a symlink from /etc/ansible to $HOME/code/ansible-mojo
  * `$ sudo ln -s /etc/ansible $HOME/code/ansible-mojo`
* Create a Vagrant VM using the image bento/xenial64 and VirtualBox as your provider
  * `$ mkdir ~/vagrant-boxes/bento_ubuntu`
  * `$ cd ~/vagrant-boxes/bento_ubuntu`
  * `$ vagrant init bento/ubuntu-16.04; vagrant up --provider virtualbox`
* Configure the VM to be accessible via host lookups on your machine (e.g., add it to your /etc/hosts)
* Add the vagrant user's private key to your authentication chain/agent for passwordless access to the VM
  * `$ ssh-add ~/vagrant-boxes/bento_ubuntu/.vagrant/machines/default/virtualbox/private_key`
* Create a RSA key to use for the ansible SSH user and populate $HOME/code/ansible/authorized_keys with it
  * `$ ssh-keygen -t rsa -f ~/.ssh/ansible_key`
  * `$ cat ~/.ssh/ansible_key > $HOME/code/ansible-mojo/authorized_keys`
* Add this new RSA key to your authentication chain/agent for passwordless access to the VM as user "ansible"
  * `$ ssh-add ~/.ssh/ansible_key`
* Install Ansible v2.2.0 from source repo on GitHub
  * `$ cd $HOME/src`
  * `$ git clone -b stable-2.2 git://github.com/ansible/ansible.git --recursive`
  * `$ cd ./ansible`
  * `$ source ./hacking/env-setup`
* Add your Vagrant VM host to Ansible's host inventory ($HOME/code/ansible-mojo/hosts)
* Test Ansible operations with your Vagrant VM
  * `$ ansible yourvmname -m setup -e ansible_ssh_user=vagrant`

## Usage

First run:

`$ ansible-playbook main.yml -e ansible_ssh_user=vagrant`

Subsequent runs:

`$ ansible-playbook main.yml`


    ------------------------------------------------------------------------

## Todo

- Create more distro-agnostic plays (e.g., same play for both CentOS and Ubuntu)
- Roles! Galaxy!

## Development

Send patches to rcrelia.github@gmail.com, or fork the project on GitHub and
send me a pull request.

## Authors

Author:: Rick Crelia<br>
