# Vagrant Docker host server

Vagrantfile for construction of docker host server of CentOS 7.

## Table of Contents

- [Getting Started](#getting-started)
  - [Ansible playbook](#ansible-playbook)
    - [Create playbook.yml](#create-playbookyml)
    - [ansible playbook setting](#ansible-playbook-setting)
  - [Vagrantfile](#vagrantfile)
    - [Create Vagrantfile](#create-vagrantfile)
    - [Vagrantfile setting](#vagrantfile-setting)
    - [Change Vagrantfile setting (Optional)](#change-vagrantfile-setting-optional)
  - [Start Vagrant](#start-vagrant)


## Getting Started

### Ansible playbook

#### Create playbook.yml

```bash
$ cp playbook.yml.dist playbook.yml
```

#### ansible playbook setting

Open the copied playbook.yml in the editor and set it.

```yaml
    hostname: <HOSTNAME>
    vim_version: <VIM_VERSION>
    docker_compose_version: <DOCKER_COMPOSE_VERSION>
    samba_user: <SAMBA_USER>
    samba_password: <SAMBA_PASSWORD>
```

- HOSTNAME: hostname of CentOS
- VIM_VERSION: cf. [Releases vim](https://github.com/vim/vim/releases)
- DOCKER_COMPOSE_VERSION: cf. [Install Docker Compose | Docker Documentation](https://docs.docker.com/compose/install/)
- SAMBA_USER: username of samba
- SAMBA_PASSWORD: password of samba

Please set vagrant for working user name and group name.

- e.g.

```yaml
    hostname: docker-host
    vim_version: v8.1.1115
    docker_compose_version: 1.24.0
    samba_user: vagrant
    samba_password: vagrant
```


### Vagrantfile

#### Create Vagrantfile

```bash
$ cp Vagrantfile.dist Vagrantfile
```

#### Vagrantfile setting

Open the copied Vagrantfile with an editor and set it.

```ruby
  # config.vm.network "public_network"
```

Uncomment the above and assign an IP address.

- e.g.

```ruby
  config.vm.network "public_network", ip: "<IP_ADDRESS_HERE>"
```

#### Change Vagrantfile setting (Optional)

Changing this setting is optional.

Please change the setting value as needed.

```ruby
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.name = "docker-host"
  end
```

- vb.memory: Set the memory allocated to VM
- vb.name:   Set the name of VM


### Start Vagrant

```bash
$ vagrant up
```

The Ansible local provisioner is executed on the first start.

cf. [Ansible local](https://www.vagrantup.com/docs/provisioning/ansible_local.html)

