update
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-update.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-update)

Provides updates for your system.

Context
-------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/robertdebock.github.io/artifacts/update.png "Dependency")

Requirements
------------

Access to a repository containing packages, likely on the internet.

Role Variables
--------------

- update_autoremove: Clean unused packages? (For APT distributions only)
- update_upgrade_command: Type of upgrade: dist, yes, safe, or full.  (For APT distributions only)
- update_cache_valid_time: Update the cache if it's older than the cache valid time (For APT distributions only)
- update_reboot: Control the desired reboot behaviour. Set to "yes" (default) or "no".

Dependencies
------------

This role can be used to prepare your system:

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-3.6|yes|yes|yes|
|alpine-3.7|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-7|yes|yes|yes|
|debian-buster|yes|yes|yes|
|debian-stretch|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-27|yes|yes|yes|
|fedora-28|yes|yes|yes|
|opensuse-42.2|yes|yes|yes|
|opensuse-42.3|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-bionic|yes|yes|yes|

Example Playbook
----------------

The simplest way possible:
```
- hosts: servers

  roles:
    - robertdebock.bootstrap
    - robertdebock.update
```

The role sets a variable so it's possible to understand if changes were made:
- update_result

Here is an example of how to use that variable:
```
- hosts: servers

  roles:
    - robertdebock.update

  tasks:
    - name: send email
      mail:
        to: sysadmin@example.com
        subject: "server {{ ansible_hostsname }} updated"
      when:
        - update_result.changed
```

Install this role using `galaxy install robertdebock.update`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
