# Sage docker repositories

Contains dockerfiles for various Sage images

## sage_docker_base

### Installation

This Dockerfile should build an image containing compiled sources of Sage in latest Ubuntu.
To build it from scratch, type
    
    docker build --tag="sagemath/sage" sage_docker_base
    
If you want to download its release, (roughly 7GB), type
    
    docker pull sagemath/sage
    
or simply continue to the next step.

### Running Sage

To start a container running sage, type
    
    docker run -it sagemath/sage
    
To start something else, like GAP, type
    
    docker run -it sagemath/sage gap
    
### Running Notebooks

To start a Jupyter or SageNotebook server you can start the container with the following command

    docker run --net="host" sagemath/sage -notebook=jupyter --no-browser
    
for the Jupyter notebook and
    
    docker run --net="host" sagemath/sage -notebook
    
for the sage notebook.


## sage_patchbot

This Dockerfile should build an image containing Sage and the testbot. To build it from scratch, type
    
    docker build --tag="sagemath/sage_patchbot" sage_patchbot
    
To start a patchbot instance, i.e., to securely run the container on your device, type
    
    docker run --name patchbot -d sagemath/sage_patchbot
    pid=$(docker inspect -f '{{.State.Pid}}' example)
    nsenter -t $pid -n iptables -A FORWARD -s 172.17.0.21 -d 8.8.8.8 -j ACCEPT
    iptables -A FORWARD -s 172.17.0.21 -j REJECT --reject-with icmp-host-prohibited
