# certification topics

Docker市场上认可度比较高的certification有Mirantis提供的DCA ( Docker Certified Associate ) \
[https://training.mirantis.com/certification/dca-certification-exam/](https://training.mirantis.com/certification/dca-certification-exam/), Mirantis在2019年将docker entreprise收购后, 将整个考证系统纳入旗下, 并在DCA中加入了K8S的内容, 同时提供k8s和openstack的证书.&#x20;

考试的具体说明在页面上有介绍, 可以预约在线考试, 有电脑和网络接通即可.  我在2020年获得DCA, 在职期间大概花了1个月时间准备, 把我的经验分享出来,参考借鉴. 所有的联系题都可以使用practices topics的docker环境进行训练.&#x20;

## Orchestration (25%)

这部分需要docker swarm cluster有熟练的了解, 理解架构中的manager和worker, 并且理解如何把单个docker container转化为可以容错稳定的service, 学会使用docker inspect观察service的运行状态. 使用yaml格式书写deployment并部署到swarm cluster上.学会如何操作service stack等等.&#x20;

### docker swarm questions&#x20;



docker create service --health-cmd



docker service -P (manager worker node ), exposed port management docker swarm

All nodes participate in an ingress routing mesh. The routing mesh enable each node in the swarm to accept connections on published ports for any service running in the swarm

ingress routing mesh

****

**Sally wants to prevent Docker Swarm encryption keys from being stored insecurely on her swarm managers. How can she tackle enforcing a lock on the swarm cluster?**

docker swarm : autolock



**Anastasia has created a container with a volume called shared-data. She wants to create a new container that can access the same data as the first container, but she wants this new container only to be able to read the data, not modify it. How can she accomplish this?**



one-time job : Amanda wants to execute a one-time job using a Docker container. However, occasionally, this job fails and needs to restart. Amanda doesn't want to restart it manually if it fails. Which command should she use to make sure that the container executes the one-time job successfully?



Which of the following commands will run a busybox container and automatically delete it once it exits?



linux feature (docker use in order to limit memory usage for containers -)



What command should we use if we want to view logs for all of the tasks in a service called my-service?



What command will help us delete a service called my-service along with all of its tasks?

docker service rm --all my-service



Kelly has a Docker swarm cluster with --autolock enabled. One of her manager nodes has become locked, and she has lost the unlock key. Fortunately, there are still some swarm nodes that are not locked. How can she obtain the unlock key from one of the unlocked nodes?

where is unlock.key



What tool should we use if we need to manage a multi-container application as a unit on a single Docker host?



Which of the following commands will allow us to add a label to a Docker Swarm node?



Which of the following namespaces is not enabled by default?



kubernetes readliveness  ( ready to service the traffic )Readiness probe :   (update in progress)Application is running but it is still loading it's large configuration files from external vendor \
exec:     command:&#x20;

* &#x20;   cat&#x20;
* /tmp/health&#x20;
* initlaDelaySeconds: 5
* periodSeconds : 5

\
to determine if the pod is ready



DaemonSets: can ensures that all nodes run a copy of a pod usecase : anti-virus kind : DaemonSet



kubectl get pods -o wide ( can see which node run the pod ) kubectl get daemonset





kind: Deployment

Taints and Tolerations :

Taints are used to repel the pods from a specific nodes in order to enter the taint worker node, you need a special pass ( toleration )

create taint : kubectl taint nodes node\_name key=value:NoSchedule

remove the taint : add - at the end





kubernets replicatset



3 manager node for cluster quorum



kubernetes rescheluer pod to another node



Docker kubernetes 4 cores how many pods Limit :\
Cpu: 2 request

Kubernetes scheduler decides the ideal node to run the pod depending on the requests and limits :

request : failed

limits: pending - no efficient resources



## Image creation and management

这部分要求掌握书写dockerfile, 如何通过dockerfile优化image, 学会使用docker 管理image的基本命令行, 并结合远程registry对image push, sign和pull等操作.



Dockerfile workdir /a b c /a/b/c



docker image prune



docker compatible OS arhictecture (docker inspect ) - images

docker build docker manifest



docker secret ( /run/secrets (can specify custom location for secrets )

## Installation and configuration

理解docker基本的安装部署和配置, 理解UCP和DTR的原理, 以及docker内部的权限管理(rbac)学会如何debug docker系统



docker daemon process in different system os dockerd dockerd.exe



difference between docker container and virtual machine



sign images and verify image signatures



How should we give a user permission to interact with the Docker daemon on a machine without giving them unnecessary additional access?

docker user group



What is an easy way to configure a client to communicate with Universal Control Plane (UCP) using client certificates?



Which storage driver is the default for current versions of CentOS/RHEL and Ubuntu





### UCP ( Universal Control Plane )

UCP node run out of disk ( troubleshooting )

a lot of image and container is running on this node



Which of the following best describes the procedure for backing up the Universal Control Plane (UCP) metadata?



docker login (UCP manager worker node )



What is an easy way to configure a client to communicate with Universal Control Plane (UCP) using client certificates?



UCP and DTR reginal mirror or cloud based storage

image no singed ( DOCKER TRUCT ENABLE = 1 docker build , docker service create, docker images inspect )



### DTR ( Docker Trusted Registry )&#x20;

joint worker node in UCP or DTR



How can you enable Docker Content Trust (DCT) in Docker Community Edition (CE)?



Which of the following is a secure method for allowing a Docker client to authenticate with a registry that uses a self-signed certificate?



Which of the following are insecure ways to allow a Docker client to authenticate against a registry that uses a self-signed certificate? (Choose two)



## Networking and security

What component of the Docker Container Networking Model (CNM) refers to a collection of endpoints that can communicate with one another?



Which network driver connects containers directly to a network stack on the host machine without any isolation? docker network



Which of the following commands will attach the tasks of a new service to an existing overlay network called my-overlay



Dns server for all containers on a host When creating an overlay network, what flag can we use to allow containers to attach to the network after it is created?



injecter container : Amanda is having some network issues and needs to do some troubleshooting. How can she inject a nicolaka/netshoot container into the sandbox of an existing container called nginx-container?

Amanda can use docker run --inject-container nginx-container nicolaka/netshoot.



overlay network in docker worker node (when no workload ) You don’t need to create the overlay network on the other nodes, beacause it will be automatically created when one of those nodes starts running a service task which requires it ( workload ).

## Storage and volume

We have a Docker host that is running low on storage. What command could help us identify how the host is using storage? docker volume



Which storage driver is the default for current versions of CentOS/RHEL and Ubuntu



persistant volume : retain is deleted : how to use persistant volume retain : released recycle delete





\
