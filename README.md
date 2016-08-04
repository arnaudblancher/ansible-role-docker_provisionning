arnaudblancher.docker_provisionning
===================================

Goal : take an ansible inventory and create one docker container for each listed hosts.

After you can deploy your favorite ansible playbook on theses docker-inventory and make easily and safely full tests in a new and clean environnement without new virtual machines.

Afer your tests, just destroy theses dockers with ansible role arnaudblancher.docker_unprovisonning 

Requirements
------------

- docker-engine

Make sure your have a docker-engine running, test with (probably as root ...)

```bash
docker info
```

### If you need, install docker-engine

Here, docker-engine 1.11 on Debian Jessie

```bash
apt-get remove docker.io python-docker
apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo 'deb https://apt.dockerproject.org/repo debian-jessie main' > /etc/apt/sources.list.d/docker.list
apt-get update
apt-get install docker-engine python-docker
```

On Ubuntu Trusty,

replace
 python-docker

by :

```bash
sudo apt-get install python-pip
sudo pip install docker-py```

Role Variables
--------------

please see [defaults/main.yml](defaults/main.yml)

Dependencies
------------

None

Example Playbook
----------------
Please see subdirectory [./demo/](./demo/)

cat demo/docker-provisionning.yml
```yaml
- name: "create all docker image and containers for all hosts listed in inventory"
  hosts: localhost
  gather_facts: no

  roles:
    - { role : arnaudblancher.docker_provisionning,
      docker_provisionning_image: "ubuntu1404",
      docker_provisionning_net: "ansible_myplateform" }
```

cat inventory/docker/000_hosts
```yaml
[mysql]
dock-mysql

[apache]
dock-apache

[all:vars]
ansible_connection=docker
```

call :
```bash
ansible-playbook  -i inventory/docker/ docker-provisionning.yml
```

License
-------

GPLv3

Author Information
------------------

Arnaud Blancher

[https://github.com/arnaudblancher/ansible-role-docker_provisionning](https://github.com/arnaudblancher/ansible-role-docker_provisionning)


