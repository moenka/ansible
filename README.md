# R&D Ansible

## Ansible

### Thoughts

* Roles change a lot of things on the target systems that aren't easy to track and less easy to revert manually. Therefor a role should by default (when including the role without configuration) clean up their own changes. If a role should provision a target it needs to be explicitly defined by setting a variable with the role name to `present`. (explicit is better then implicit)

## Usage

### Testing

To bring up the environment

## Setup

### SSH

For research and development it's easier to disable ssh key checking (shouldn't be used in production though).
```
Host *.vagrant
    StrictHostKeyChecking no
    UserKnownHostsFile=/dev/null
    User root
    LogLevel ERROR
```

### Vagrant

#### Plugins

##### vagrant-hostmanager

`vagrant plugin install vagrant-hostmanager`

Passwordless hosts update with visudo:
```
# vagrant-hostmanager
Cmnd_Alias VAGRANT_HOSTMANAGER_UPDATE = /bin/cp */.vagrant.d/tmp/hosts.local /etc/hosts
%sudo ALL=(root) NOPASSWD: VAGRANT_HOSTMANAGER_UPDATE
```

### Approx

The debian machines expect an apt mirror/proxy to run on 192.168.33.1:9999 (the vagrant interface of the vm host) so it's recommended to install an approx on the vm host.

## Sources

* [6 practices for super smooth Ansible experience](http://hakunin.com/six-ansible-practices)
