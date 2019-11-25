Configuration to help setup my test environment for samba development. I am currently using Fedora 31.

I use the 192.168.147.0/16 subnet to create my test containers and my helper script creates the containers with the name vm147-$n and ip address 192.168.147.$n where $n is the container number. The helper script c_samba creates builds using a template fedora30_samba_common. You will have to build the samba template before you can continue.

1) Setup the podman bridge.
	- install podman 
	- Edit /etc/cni/net.d/87-podman-bridge.conflist and change the "subnet" and "gateway". Check confs//etc/cni/net.d/87-podman-bridge.conflist for my setup.

2) Edit the helper script for your setup.
 	- change container_name and the --ip= line in the command argument to reflect your ip address used.
	- Change the line "--volume /data/sprabhu/docker_home:/home/sprabhu \". Here directory /data/sprabhu/docker_home on host is mounted at /home/sprabhu. ie. I use a separate folder as my home folder within docker.
	- The line "--volume /data:/data \"  mounts directory /data from host into /data in container. This contains my git repos which are symlinked to from my home directory mounted in the earlier line. Modifications I make in the git repo on my host machine are immediately reflected in the container allowing me to test builds conveniently.
	
3) Create a symlink to the file in a directory in $PATH. 

4) We then generate the template file by cd-ing into containers_template/samba_devel/ and editing Dockerfile
	- line "RUN	groupadd -g 4505 sprabhu" and "RUN	useradd -u4505 -g sprabhu sprabhu" Add myself as a user on the container while reflecting the uid/gid on my host system. This means that changes can be made seamlessly on both host and container without permission issues.
	- The template also has users test1 and test2 which have been included in smbpasswd with password 'x'. These are used to test the samba server.
	- The test samba server has a folder /test created which are used to test the setup.
	- Edit smb.conf in the directory if you want to make changes to the samba server created.
	- The line "RUN     ln -s /home/sprabhu/root-dev /root/dev" is for my own setup and can be deleted.
	- Change the USER and WORKDIR folders to reflect your own account.
	- Once the files have been modified, create the template file by running the script build.sh

5) Now create your own container.
	- Calling "c_samba 11", creates a container vm147-11 with ip address 192.168.147.11 which contains a samba devel environment. I usually create 2 environments with 1 server and one client to run torture tests.
