# ansible-mojo

## Description

A simple introductory demo of Ansible playbook operations.

For a more in-depth discussion, check out this [blog post](https://randops.org/2016/10/26/ansible-shenanigans-part-i/).

## Installation

* Clone this repo down to the system you'll be running Ansible from and make it your working directory
```bash
$ cd $HOME/code
$ git clone https://github.com/rcrelia/ansible-mojo.git
$ cd ansible-mojo
```
* Create a symlink from /etc/ansible to $HOME/code/ansible-mojo
```bash
$ sudo ln -s /etc/ansible $HOME/code/ansible-mojo
```
* Create a Vagrant VM using the image bento/xenial64 and VirtualBox as your provider
```bash
$ mkdir ~/vagrant-boxes/bento_ubuntu
$ cd ~/vagrant-boxes/bento_ubuntu
$ vagrant init bento/ubuntu-16.04; vagrant up --provider virtualbox
```
* Configure the VM to be accessible via host lookups on your machine (e.g., add it to your /etc/hosts)
* Add the vagrant user's private key to your authentication chain/agent for passwordless access to the VM
```bash
$ ssh-add ~/vagrant-boxes/bento_ubuntu/.vagrant/machines/default/virtualbox/private_key
```
* Create a RSA key to use for the ansible SSH user and populate $HOME/code/ansible/authorized_keys with it
```bash
$ ssh-keygen -t rsa -f ~/.ssh/ansible_key
$ cat ~/.ssh/ansible_key > $HOME/code/ansible-mojo/authorized_keys
```
* Add this new RSA key to your authentication chain/agent for passwordless access to the VM as user "ansible"
```bash
$ ssh-add ~/.ssh/ansible_key
```
* Install Ansible v2.2.0 from source repo on GitHub
```bash
$ cd $HOME/src
$ git clone -b stable-2.2 git://github.com/ansible/ansible.git --recursive
$ cd ./ansible
$ source ./hacking/env-setup
```
* Add your Vagrant VM host to Ansible's host inventory ($HOME/code/ansible-mojo/hosts)
* Test Ansible operations with your Vagrant VM
```bash
$ ansible yourvmname -m setup -e ansible_ssh_user=vagrant
```

## Usage

First run:

```bash
$ ansible-playbook main.yml -e ansible_ssh_user=vagrant
```

Subsequent runs:

```bash
$ ansible-playbook main.yml
```

## Todo

- Create more distro-agnostic plays (e.g., same play for both CentOS and Ubuntu)
- Roles! Galaxy!

## Development

Send edits/ideas to rcrelia.github@gmail.com, or fork the project on GitHub and
send me a pull request.

## Authors

Author:: Rick Crelia

## License

Copyright:: Copyright (c) 2014 Rick Crelia<br>
License:: Apache License, Version 2.0

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
