Redis does not support NATed networking mode. For Docker to run successful, we need to use "host networking mode" by running the Docker image into a container.

For example.

https://redis.io/topics/cluster-tutorial

https://hub.docker.com/_/redis/

docker pull redis

docker run -dt --name redis --network host redis

The above command enable to deploy redis Docker container associate with host networking mode instead of NATed.

The current Ansible playbooks was developed and test using Vagrant to create 3 VM(s) and the Ansible configuring 3 nodes into Master-Slave mode of 6 nodes.

This means that each node should have a Master and slave.

Suggestion:
==========

Users should be able to clone the repo from my GitHub "linh5847" and follows the steps.

PreRequisites:-

Install VirtualBox
Install Vagrant
Install Ansible

I'm using VirtualBox 6, Vagrant 2.2.9, Python 3.6 and Ansible 2.9 for developing and test the Redis cluster.

Methods:

Clone the redis git repo from my GitHub account as follows:-

git clone git@github.com:vntechsol/redis.git

cd redis

vagrant status

vagrant up

I strongly suggestion to use MAC or Linux Laptop instead of Windows.