# Template of Ansible Role Tests with Docker

This is a simple test template for Ansible role that uses Docker.

## Supported container distros and versions

| Distro | Versions          |
|:-------|:------------------|
|Ubuntu  |14.04, 15.10, 16.04|
|Debian  |Wheezy, Jessie     |
|Fedora  |22, 23             |
|CentOS  |6, 7               |
|OpenSUSE|13.2               |

## Installation

Create a role and replace the `tests` directory like this:

```bash
$ ansible-galaxy init new-playbook
$ cd new-playbook
$ rm -rf tests
$ git clone https://github.com/kjtanaka/ansible-role-tests-with-docker.git tests
$ cd tests
```

## How to use

Take a look at `Makefile`, and update variables as you need. The default variables are
set for the default environment of the Docker Toolbox on Mac OS X.

```bash
# Test Playbook
$ make provision
# or
$ make

# Log into the container
$ make ssh

# If you want to destroy container and provision it again
$ make reprovision
# or
$ make clean-ps && make provision

# Clean all
$ make clean
```

Basically, everytime you update your role, you just need to execute `make provision` or
`make`, and then when you want to test the role from scratch, execute `make reprovision`.
After you finish everything, then clean it by `make clean`.

## License

MIT license.

## Reference

Those Dockerfiles are inspired by these links:

- [tutumcloud/tutum-centos](https://github.com/tutumcloud/tutum-centos.git)
- [Dockerizing an SSH daemon service](https://docs.docker.com/engine/examples/running_ssh_service/)
