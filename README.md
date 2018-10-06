# toolkit-ansible-role
Ansible role for RNA-Puzzles Toolkit. Contains ansible-container config and an example playbook.

Currently the role supports Ubuntu only. It was tested with Ubuntu Xenial.

# Docker image
This Ansible role is used to create Docker images which are available in Docker Hub as `rnapuzzles/toolkit`. If you are here just to use RNA-Puzzles Toolkit, you can use that image directly:
```
docker pull rnapuzzles/toolkit
docker run --publish 8888:8888 --name toolkit rnapuzzles/toolkit
```

The Jupyter notebook with RNA-Puzzles Toolkit examples will be available in your browser at address `http://localhost:8888`. The default password is `demo`. To kill the running container, execute:
```
docker kill toolkit
```

To access RNA-Puzzles Toolkit directly, start Docker image within a shell:
```
docker run --interactive --tty rnapuzzles/toolkit /bin/bash
```

# How to build and use Docker container image with RNA-Puzzles Toolkit
The repository contains configuration for ansible-container which uses roles and docker-compose-like syntax to describe creation of container images using Ansible. 

## Step 1: Install ansible-container (virtualenv recommended)
```
pip install ansible-container[docker]
```

## Step 2: Build the image
```
cd toolkit-ansible-role
ansible-container --debug build
```

## Step 3: Run the container
```
docker run --publish 8888:8888 --name toolkit rnapuzzles/toolkit
```

To kill the running container, execute:
```
docker kill toolkit
```

## Step 4: Explore RNA-Puzzles Toolkit
Open `http://localhost:8888` browser and use default `demo` password. Explore the various Jupyter notebooks which demonstrate capabilities of RNA-Puzzles Toolkit. 

## Step 5 (optional): Directly use RNA-Puzzles Toolkit
You may wish to override default command of running Jupyter notebooks and work with the RNA-Puzzles Toolkit directly. To do so, run Docker with a shell command:
```
docker run --interactive --tty rna-puzzles-toolkit /bin/bash
```

# How to install RNA-Puzzles Toolkit in a cloud
The steps below describe a process of installation of RNA-Puzzles Toolkit on a cloud host. The assumption is that the machine has Ubuntu installed with `ubuntu` user having `sudo` capabilities. Please change `site.yml` to suit the configuration for your own needs.

## Step 1: Install Ansible
Install Ansible using your OS way of package management.

## Step 2: Configure your host
Edit `/etc/ansible/hosts` and add group `ubuntu` with the IP of your cloud-enabled machine:
```
[ubuntu]
192.168.1.1
```

## Step 3: Configure your host
For Ansible to work, you need to be able to connect via SSH in a passwordless manner as `ubuntu` user. And you need to have Python installed on the machine. Make sure these requirements are met.

## Step 4: Apply Ansible role to the host
```
cd toolkit-ansible-role
ansible-playbook site.yml
```
