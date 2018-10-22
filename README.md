# docker
<h1>Docker Notes</h1>

Start docker:

sudo systemctl start docker

<pre>
docker swarm init	#init swarm

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

[isaac@localhost DockerLab]$ docker stack rm getstartedlab
[isaac@localhost DockerLab]$ docker-machine ssh myvm2 "docker swarm leave"
[isaac@localhost DockerLab]$ docker-machine ssh myvm1 "docker swarm leave --force"
[isaac@localhost DockerLab]$ eval $(docker-machine env -u)
[isaac@localhost DockerLab]$ docker-machine ls
[isaac@localhost DockerLab]$ docker-machine stop myvm1
[isaac@localhost DockerLab]$ docker-machine stop myvm2
</pre>
