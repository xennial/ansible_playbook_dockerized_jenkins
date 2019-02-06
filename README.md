Ansible Script for Provisioning Dockerized Jenkins on Ubuntu

This ansible playbook is designed to install Jenkins docker container on to a digital ocean Ubuntu 16 instance. Though it will likely work with any cloud provider (and Debian system), it has only been tested on Digital Ocean.

TLDR
How to run:

Create a hosts/inventory file in the root of this directory for Ansible and run the command below:

ansible-playbook -i your_hosts_file site.yml -u youruser --private-key ~/.ssh/your_private_key 

Change youruser and your_private_key to your own values

The playbook does the following

1. Installs Docker-CE following the steps laid out in this official guide

https://docs.docker.com/install/linux/docker-ce/ubuntu/


2. Sets up the Docker port work correctly following the official docker documentation

3. Pulls down and sets up the official Jenkins docker container and maps the socket volume on to that of the host machine. This is to avoid issues of running Docker in Docker. For more information on the problems with Docker in Docker please see this article
https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/
The below is also a very useful article to read if you'd like to do this set up manually:
https://getintodevops.com/blog/the-simple-way-to-run-docker-in-docker-for-ci

4. Runs the Jenkins container on port 8080. Mounts also bind mounts jenkins settings to the directory /var/jenkins_docker_config on the host

5. Installs Jenkins plugins??


6. To do /Future updates
Make second internal network address in docker daemon.json dynamic with something like:
ifconfig docker0 | grep 'inet addr:' | cut -d: -f2

Final notes

Use this user data when you first create the droplet to avoid having to install python

#cloud-config

runcmd:
 - apt-get install -y python2.7
 - ln -s /usr/bin/python2.7 /usr/bin/python
 
 

You can check the integrity of the docker-ce package by checking the GPG key. Instructions are listed here about half way down the page:
https://docs.docker.com/install/linux/docker-ce/ubuntu/
 

If you require more security consider using this role:
<insert link here>
