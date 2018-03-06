Ansible Role - jdk
==================

This playbook installs Oracle [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Platforms
---------

CentOS 6.7 is the only platform that is supported and tested so far.

Role Variables
--------------

- Check out [defaults/main.yml](defaults/main.yml)

Dependencies
------------

None.

Installation
------------

Regular installation:

```
ansible-galaxy install RDI2.jdk
```

Installation to a specific directory(e.g. roles/):

```
ansible-galaxy install -p roles/ RDI2.jdk
```

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: RDI2.jdk }

License
-------

MIT License.

Author Information
------------------

- Koji Tanaka, RDI2
