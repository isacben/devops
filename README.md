# docker
<h1>Docker Notes</h1>

Start docker:

<pre>sudo systemctl start docker</pre>

<h2>Basic Commands</h2>

<pre>
#list all the containers
docker container ls -a

#list all the images
docker image ls -a
</pre>

<h2>Other Important Commands To Remember</h2>

Run a container which exits after the execution of the command:

<pre>docker container run alpine echo "hello from alpine"</pre>

Run a container and stay inside the container's command line:

<pre>docker container run -it alpine /bin/sh</pre>

This starts a container and leaves it running to be able to execute commands:

<pre>
docker container run -it alpine /bin/ash

#if we exited, you can restart the same container:
docker container start <container ID>

#and then execute commands:
docker container exec <container ID> ls
</pre>

<h2>Working With Swarms</h2>

<pre>
#init swarm
docker swarm init

#Create the virtual machines
docker-machine create --driver virtualbox myvm1
docker-machine create --driver virtualbox myvm2

#Show the virtual machines
docker-machine ls

#Add a manager
docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1 ip>"

#ADd a worker
docker swarm join --token SWMTKN-1-3na6u4b5nh3x7a2d8daqj60stj0e6rod7ou8uiidxj78g4qkja-7p8mjno4xq6m8nwjd1haw900m 192.168.99.100:2377	#output of the previous command
docker-machine ssh myvm2 "docker swarm join --token <token> <ip>:2377"	#Full command format

#See the nodes by running this command in the manager
docker-machine ssh myvm1 "docker node ls"

#Configure the server to talk to the manager
docker-machine env myvm1
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://192.168.99.100:2376"
export DOCKER_CERT_PATH="/Users/sam/.docker/machine/machines/myvm1"
export DOCKER_MACHINE_NAME="myvm1"
eval $(docker-machine env myvm1)


#Restart the virtual machines
docker-machine start myvm1
docker-machine start myvm2

#Shutdown the SWARM
docker stack rm getstartedlab
docker-machine ssh myvm2 "docker swarm leave"
docker-machine ssh myvm1 "docker swarm leave --force"
eval $(docker-machine env -u)
docker-machine ls
docker-machine stop myvm1
docker-machine stop myvm2
</pre>
