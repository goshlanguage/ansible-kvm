# Ansible-KVM

A playbook to setup KVM on Centos 7, including a management tool called WebVirtManager
WebVirtManager is a third party tool that:
  - Defines VMs per XML Templates generated for you through a web interface
  - Allows you to remote console to your VM through HTML (noVNC)
  - Allows you to manage your guest VMs (add/reduce ram/cpu/hdd power on/off suspend)

Getting started with this playbook, you should edit the hosts to match your hosts file.
Should you wish to move the app_path for WebVirtMgr, you may do so by changing the app_path variable.

### Installation
To install KVM on Centos7 with this playbook:
```ssh
git clone https://github.com/ryanhartje/ansible-kvm.git
cd ansible-kvm
vim deploy.yml # edit hosts
ansible-playbook deploy.yml
```

### Post Installation

Currently, this project is missing automated steps for TCP authentication, as well as the login user.

Because of this,  you will need to create these two accounts. 

To setup your TCP account, use will use saslpasswd2:
```sh
$ sudo saslpasswd2 -a libvirt
Password: xxxxxx
Again (for verification): xxxxxx
```

To setup your login user, you must navigate to your project folder, and run:
```sh
./manage.py createsuperuser
WARNING:root:No local_settings file found.
Username: user
Email address: user@mail.com
Password:
Password (again):
```

### Usage

Currently, we are not actually reverse proxying WebVirtMgr, as it is more secure to connect over an SSH Tunnel, for encryption purposes. 


Here is an example of an SSH tunnel that will allow us to access webvirtmgr at http://localhost:8000

```sh
$ ssh user@server:port -L localhost:8000:localhost:8000 -L localhost:6080:localhost:6080
```

