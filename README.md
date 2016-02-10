Role Name
=========

Installs couchbase DB - http://www.couchbase.com/

Requirements
------------

Define Ansible host inventory as example below in order to configure cluster.
````
[couchbase-master]
couchbase01 ansible_ssh_host=192.168.202.201

[couchbase-servers]
couchbase02 ansible_ssh_host=192.168.202.202
couchbase03 ansible_ssh_host=192.168.202.203
````

Vagrant
-------
Spin up Environment under Vagrant to test. This environment has 3 nodes (1-master and 2-members)
````
vagrant up
````

Usage
-----

###### Non-Vagrant
Login to WebUI using defined owncloud_admin_user and owncloud_admin_pass vars (http://iporhostname:8091)

###### Vagrant
Login to WebUI using defined owncloud_admin_user and owncloud_admin_pass vars (http://127.0.0.1:8091)

Role Variables
--------------

````
---
# defaults file for ansible-couchbase
couchbase_admin_pass: 'P@55w0rd'
couchbase_admin_user: 'admin'
couchbase_cli: '/opt/couchbase/bin/couchbase-cli'
couchbase_cluster_ram_multiplier: 0.5
couchbase_cluster_ram_quota: '{{ (ansible_memtotal_mb | int * couchbase_cluster_ram_multiplier) | round | int }}'
couchbase_config_cluster: false  #defines if couchbase cluster should be initialized
couchbase_debian_package: 'couchbase-server-community_{{ couchbase_version }}-{{ ansible_distribution|lower }}{{ ansible_distribution_version }}_amd64.deb'
couchbase_debian_package_dl: 'http://packages.couchbase.com/releases/{{ couchbase_version }}/'
couchbase_version: '4.0.0'
````

Dependencies
------------

None

Example Playbook
----------------

#### GitHub
````
---
- name: provisions Couchbase
  hosts: all
  become: true
  vars:
    - couchbase_config_cluster: true
  roles:
    - role: ansible-couchbase
  tasks:
````
#### Galaxy
````
---
- name: provisions Couchbase
  hosts: all
  become: true
  vars:
    - couchbase_config_cluster: true
  roles:
    - role: mrlesmithjr.couchbase
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com