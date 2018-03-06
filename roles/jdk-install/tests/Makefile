################################################################################
#
# Configuration of Docker machine
#
docker_machine = default
docker_machine_ip = 192.168.99.100
docker_ssh_port = 2223
docker_ssh_pubkey_path = ~/.ssh/id_rsa.pub
docker_ssh_privkey_path = $(shell echo $(docker_ssh_pubkey_path) | sed 's/.pub//g')

#
# Available distros and versions
#
#docker_image_distro = ubuntu_1404
#docker_image_distro = ubuntu_1510
#docker_image_distro = ubuntu_1604
#docker_image_distro = debian_jessie
#docker_image_distro = debian_wheezy
#docker_image_distro = fedora_22
#docker_image_distro = fedora_23
#docker_image_distro = centos_7
docker_image_distro = centos_6
#docker_image_distro = opensuse_13

################################################################################
docker_ssh_pubkey = $(shell cat $(docker_ssh_pubkey_path))
docker_config = $(shell docker-machine config $(docker_machine))

all: provision

inventory:
	echo docker-container ansible_port=$(docker_ssh_port) ansible_user=root ansible_host=$(docker_machine_ip) ansible_ssh_private_key_file=$(docker_ssh_privkey_path) > inventory

image: inventory
	docker $(docker_config) images |grep ansible_test_$(docker_image_distro) || docker $(docker_config) build -t ansible_test_$(docker_image_distro) -f Dockerfile.d/$(docker_image_distro) .

instance: image
	docker $(docker_config) ps |grep $(docker_image_distro)_instance || docker $(docker_config) run -p $(docker_ssh_port):22 --name=$(docker_image_distro)_instance -e AUTHORIZED_KEYS="$(docker_ssh_pubkey)" -dt ansible_test_$(docker_image_distro)

clean-ps:
	docker $(docker_config) stop $(docker_image_distro)_instance
	docker $(docker_config) rm $(docker_image_distro)_instance

clean-all: clean-ps
	docker $(docker_config) rmi ansible_test_$(docker_image_distro)
	rm inventory

clean: clean-all

ssh:
	ssh -p $(docker_ssh_port) -i $(docker_ssh_privkey_path) -o StrictHostKeyChecking=no root@$(docker_machine_ip)

provision: instance
	ansible-playbook -i inventory test.yml

reprovision: clean-ps provision
