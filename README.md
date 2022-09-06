# ansible-docker-container
A simple html demo site running on docker container created using ansible

# playbook.yml
```
---
- name: "Setting up docker container on client server using ansible"
  become: true
  hosts: all
  vars:
    packages:
      - docker
      - pip
  tasks:

    - name: "installing docker and pip"
      yum:
        name: "{{packages}}"
        state: present

    - name: "installing dependencies"
      pip:
        name: docker-py
        state: present

    - name: "restarting & enabling docker service"
      service:
        name: docker
        state: restarted
        enabled: true

    - name: "Creating httpd container"
      docker_container:
        name: apache
        image: hemanthsaju7/ansible_docker_container:latest
        ports: "80:80"
``` 

# hosts
```
[aws]
<private_ip> ansible_user="ec2-user" ansible_port=22 ansible_ssh_private_key_file="key.pem"
```
