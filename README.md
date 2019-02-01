This ansible playbook is designed to install Jenkins docker container on to a digital ocean Ubuntu 16 instance. Though it will likely work with any cloud provider, it has only been tested on Digital Ocean

The playbook does the following

1. Installs Docker-CE following the steps laid out in this excellent guide

https://getintodevops.com/blog/building-your-first-docker-image-with-jenkins-2-guide-for-developers?rq=jenkins

2. Sets up the Docker port work correctly following the official docker documentation

3. Pulls down and sets up the official Jenkins docker container and maps the socket volume on to that of the host machine. This is to avoid issues of running Docker in Docker. For more information on the problems with Docker in Docker please see this article
https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/

4. Installs Jenkins plugins??

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
