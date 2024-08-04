# Introduction-to-Containers-Kubernetes-and-OpenShift-V2

## General Information

### Course Overview

This course introduces the core concepts of Containers and Kubernetes and explains how containers differ from virtual machines. It also covers the importance of containers in cloud computing as well as the emerging ecosystem of related technologies such as Docker, Kubernetes, OpenShift, Istio and Knative.

### Who Should Take This Course
This course is of interest to anyone who wants to be a cloud practitioner and who uses container skills as a developer, architect, system engineer, network specialist or other relevant role.  This course material also serves the needs of those who perform the tasks of advising, building, moving and managing cloud solutions. 

### Pre-requisite

We have created this course so that anyone with a basic understanding of cloud computing will be able to learn about Containers and Kubernetes. 

## Learning Objectives
After completing this course you will be able to:

- Understand the benefits of containers
- Build and run a container image
- Understand Kubernetes architecture
- Write a YAML deployment file
- Expose deployment as a service
- Manage applications with Kubernetes
- Use ReplicaSets, auto-scaling, rolling updates and service bindings
- Understand the benefits of OpenShift, Istio and other important tools

## Syllabus
Course Syllabus

### Module 1: Understanding the Benefits of Containers 

- Introduction to Containers
- Introduction to Docker
- Building Container Images
- Using Container Registries
- Running Containers

### Module 2: Understanding Kubernetes Architecture

- Understanding Container Orchestration
- Understanding Kubernetes Architecture
- Introduction to Kubernetes Objects
- Using Basic Kubernetes Objects
- Using the kubectl command
- Leveraging Kubernetes

### Module 3: Managing Applications with Kubernetes

- Using ReplicaSets
- Using Autoscaling
- Understanding Rolling Updates
- Understanding ConfigMaps and Secrets
- Using Service Bindings

### Module 4 - The Kubernetes Ecosystem

- The Kubernetes Ecosystem
- Introduction to Red Hat OpenShift
- Red Hat OpenShift and Kubernetes
- Builds
- Operators
- Istio

## Module 1

### What are Containers?
A container is an executable unit of software. Basically, what your program needs to run packed in one place so it can be executed anywhere.

Imagine old shipping methods. Too much wasted space. Look at modern shipping methods. Neat and clean. This is the idea of containers.
- Easy to Move
- Light weight
- Fast

Virtual machine is an emulation of a physical computer. VMs enable teams to run what appear to be multiple machines, with multiple operating systems, on a single computer. VMs interact with physical computers by using lightweight software layers called hypervisors. Hypervisors can separate VMs from one another and allocate processors, memory and storage among them.

VMs are also known as virtual servers, virtual server instances and virtual private servers.

Containers are a lighter-weight, more agile way of handling virtualization—since they don’t use a hypervisor, you can enjoy faster resource provisioning and speedier availability of new applications. 

Rather than spinning up an entire virtual machine, containerization packages together everything needed to run a single application or microservice (along with runtime libraries they need to run). The container includes all the code, its dependencies and even the operating system itself. This enables applications to run almost anywhere—a desktop computer, a traditional IT infrastructure or the cloud.

Containers use a form of operating system (OS) virtualization. Put simply, they leverage features of the host operating system to isolate processes and control the processes’ access to CPUs, memory and desk space.

Use cases for containers:
- Microservices (loosely coupled and independently deployable services)
- DevOps (build, ship and run software)
- Hybird, multi-cloud (run consistently across environments)
- Application modernizing and migration

### Intro to Docker
Docker is a software platform for building and running containers.

Docker image and Docker container are used interchangeable for image and container.

One of the most used Docker tools is Docker CLI.

Common Docker commands:
1. docker build
  - Creates container images
  - Requires a Dockerfile
  - Tags, or names, iamges
2. docker tag
  - Names Images
  - Doesn't overwrite existing Images
  - Creates a new Tag that points to images
3. Docker images
  - Lists all images (repo, tags, size)
4. Docker run
  - Runs a container
  - Suited for testing images
5. Docker push
6. Docker pull
  - Used for storing images in a remote location and then retrieving those images

Docker is a container runtime, a software that executes containers.

Hardware-> OS-> Container Runtime-> Applications (App1, App2, App3...)

### Building Container Image
Dockerfile -> Image -> Container

A dockerfile is the blueprint for an image, outlines steps to build the image.

An Image is an immutable file that contains the source code, libraries, and dependencies for an application to run. In a sense a template or blue print for containers. A snapshot of a container. (READ-ONLY file)

A Container is an running Image. A write layer is written on top of Image to enable containers to execute.

A Dockerfile is a text file that contains all instructions/commands to create the Image

Images are built layer by layer with each Instruction building an Image layer.

Dockerfiles start with FROM instruction. FROM instruction contains/defines base image. The start point for the rest of the Image.

The RUN instruction executes commands.

The ENV command allows you to set environment variables.

ADD and COPY commands allow you to Copy files and directories. COPY only for localfiles and directories. ADD can add files from remote URL

CMD can only be used once and it provides default command for container execution

DockerFile example:

FROM ubuntu:18.04

COPY ./app

RUN make /app

CMD python/app/app.py

### Container Registry
Is the location where container images are stored and retrieved. Registries can be public or private. Most enterprises use a private registry.

Can be HOSTED or SELF-HOSTED. HOSTED are deployed by creator for example IBM CLOUD, we don't need to deploy the image, just use it.

When storing an Image in a Registry we say PUSH. When we install an Image from the Registry we use PULL.

Image naming: hostname/repository:tag

Tag is a version number or OS built on.

### Running Containers
FROM node:9.4.0-alpine

COPY app.js

COPY package.json .

RUN npm install &&\ apk update &&\ apk upgrade

CMD node app.js

docker build -t my-app:v1 .
- -t indicates tag option, name we want to give to the image
- repository name: my-app
- tag is version, v1
- . at end means current working directory ( we can also write a full path to the build Context )

docker images
- Shows my-app image (repo, tag, image id, created, size)

docker tag my-app:v1 second-app:v1
- it takes first image we want to tag, my-app:v1
- it takes second image we want to apply second-app:v1
- Once we run it, we see 2 images diff repo but same image ID

docker images

docker run my-app:v1
- Hello, world!

docker push my-app:v1

If we go on Dockerhub, we can view the image.

## Module 2

### Container Orchestration
- Provisioning and deployment
- Availability
- Scaling
- Scheduling to infrastructure
- Rolling updates
- Health checks

Kubernetes is:
- open source, various companies and people contribute to it and the code can be found out online.
- Container Orchestration Platform & Facilitates declarative management
- Possesses a Growing Ecosystem
- Widely Available

Kubernetes is not / does not:
- traditional, all-inclusive platform as a service (PaaS)
- limit the types of applications
- deploy source code or build applications
- prescribe logging, monitoring, or alerting solutions
- provide built-in middleware, databases, or other services

### Kubernetes Architecture
A deployment of Kubernetes is called a Cluster

kube-api-server exposes Kubernetes API. All communication in the cluster utilizes this API.

etcd. Highly available key-value store. Contains all cluster data. Source of truth for the state in a kubernetes cluster.

kube-scheduler. Assigns newly created Pods to nodes. Determines where workloads should run within the Cluster.

kube-controller manager runs all the controller processes that monitor clustor state and makes sure it matches desired state

cloud-controller manager runs controllers that interact with underlying cloud providers. Links clusters into a cloud provider's API

Nodes are worker machines in Kubernetes. User applications are run on Nodes. They can be Virtual or Physical Machine. Managed by Control Plane. They aren't kubernetes but by the provider. Contains necessary services to run application

Kubelet communicates with API server, ensures POD and their associated containers are running. Reports to the control plane on health and status.

Container runtime downloads images and runs containers, kubernetes implements an interface so that this component is pluggable, docker is a well-known runtime.

Kubernetes proxy is a network proxy that runs on each node and a cluster. It contains network rules that allow communication to Pods. This communication can come in or outside the cluster.

What is a control loop?

Non-terminating loop that regulates the state of a system, for example a thermostat that maintains the desired temperature in the room.

Controllers:
- Monitor state of a cluster
- Take action to ensure the actual state matches the desired state
- Communicate with the API server to initiate these actions
- Track Kubernetes objects and ensure that the desired state is achieved

### Kubernetes Objects
Objects are persistent entities in Kubernetes meaning once created Kubernetes ensures they keep existing.

Example of Kubernetes Objects:
- Pods
- Namespaces
- Deployments
- Configmaps
- Volumes

To work with these objects (create, update, delete) you use Kubernetes API. The most common way to perform these actions is to use the "kubectl" command-line interface.

Kubernetes Objects consist of 2 main fields, SPEC that dictates the desired state for this object. STATUS which is provided by Kubernetes to describe the current state of the object.

The goal is for the desired state to match the current state.

Namespaces provide a convenient way to virtualize a physical cluster. One Cluster can appear to be several distinct clusters. Very useful for cost saving purposes or maintaining multiple projects that we want segregated.

- kube-system namespace is present to hold some of these components.
- Default namespace can be used to hold the users applications
- Additional namespaces can be created to keep things separated, ex namespace for teams, projects, apps and so on..
- Namespaces provide a scope for the name of objects. Each object has a name that must be unique for that resource type within that namespace.

Labels are key/value pairs that can be attached to objects in order to identify those objects. They do not have to be UNIQUE. Labels area used to keep things grouped adn organized.

This is where selectors come into play. Label selectors are the core grouping primitive in Kubernetes. They enable you to identify a set of objects.

### Basic Kubernetes Objects
#### POD:
- Simplest unit in Kubernetes
- Represents processes running in your cluster
- Encapsulates a container or sometimes multiple
- Replicating a Pod serves to scale an application horizontally

YML FILE:

apiVersion: v1
kind: Pod
metadata:
    name: nginx
spec:
    containers:
    - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80

- kind field is the kind of object we want to create.
- spec fields depends on kind of object we want to create, a pod spec must contain at least one container.
- name is the name of container
- image is the image of container
- ports array lists ports to expose container

#### ReplicaSet:
- Maintains a set of identical Pods
- kind: ReplicaSet
- replicas: number of replicas (of pods) to be running at any given time
- pod template so we know the pods to be created by the ReplicaSet
- selector: matchLabels: app: nginx . Labels aren't unique remember? We tell program to find app: nginx and once it does to create the replicas

### Kubernetes CLI (Kubectl)
- Key Tool for working with Kubernetes
- Provide functionality for working with clusters and workloads running on clusters
- Several different command types including declarative and imperative

#### Imperative:
- Quickly create, update, and delete Kubernetes objects
- Easiest to learn
- Doesn't provide an audit trail
- Not very flexible

Imagine you want to deploy a container with the same details of running one and there is no configuration files. You would have to guess and think hard right? Maybe call the person who ran that container. This is why we need a template.

- Use Configuration template
- Specify an operation such as create, replace, or delete

#### Declarative commands:
- Configuration files define one or more objects
- No operation is specified (Needed operations are inferred by kubectl)
- Works on files and directories
- Configuration files define desired state, and Kubernetes actualizes that state
- Preferred method for production systems

We have a configuration file, shared with developers. Even if one of developers miss updating the file we can still add them to the file and it works just fine.

Note: kubectl is pronounced as cube control

### Using Kubernetes
- Apply command: kubectl apply -f file.yaml
- It makes state of cluster match with one in the provided files
- It is fully declarative, we don't specify steps
- Viewing Resources:
1. kubectl get deployments --namespace kube-system
2. kubectl describe deployment kube-dns-amd64 --namespace kube-system

They are both namespace scoped.

Get command lists all deployments in the kube-system namespace. (Kube-system is a namespace for objects created by the Kubernetes system.

Describe command shows details of a specific deployment in the kube-system namespace

Lets run an example, here is nginx.yaml file:

apiVersion: v1
kind: Pod
metadata:
    name: nginx
spec:
    containers:
    - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80

- $ kubectl apply -f nginx.yaml
- deployment.apps/nginx-deployment created
- Object created, but is it running successfuly?
- kubectl get deployment
- We see 3/3 ready, up-to-date, available. Yep it works

## Module 3 - Manage Kubernetes Applications

### ReplicaSet
- Replicate pods for redundancy ( add/delete pods as needed )
- Maintain desired state
- Supersede replica controller
- It doesn't own any Pods, it uses their Labels to decide
- An ReplicaSet is created automatically when you create a deployment. It replicates to a single POD

To create one from scratch:
- apply a YAML file with "kind" attribute set to "ReplicaSet"
- It is recommended to create a deployment instead
- "rs" is short form for ReplicaSet

Scale existing deployment:
- $ kubectl create -f deployment.yaml
- $ kubectl get pods (shows created PODS)
- $ kubectl get deploy (gets deployment)
- kubectl scale deploy hello-kubernetes --replicas=3
- kubectl get pods (notice we have 2 more pods now)

How do we know it is working? Delete a POD. EZ PZ
- kubectl get pods
- kubectl delete pod hello-kubernetes-5655b546f8-5mflw

### AutoScaling
- ReplicaSet works with a set number of pods
- Horizontal Pod Autoscaler (HPA) enables scaling up and down as needed
- Can configure based on desired state of CPU, memory, etc..

How to create an Autoscaler?
- kubectl get pods
- kubectl get rs (rs = ReplicaSet remember)
- kubectl autoscale deploy hello-kubernetes --min=2-- max=5 --cpu-percent=10
- min = minimum number of pods, max is maximum number of pods
- cpu-percent is trigger to create pods, it looks at usage of cpu %
- kubectl get pods (behind scene it scales up and down depending on CPU usage)
- kubectl describe rs hello-kubernetes-5655b546f8
- kubectl get hpa

Otherway is to create a manually autoscale YAML file. kind: HorizontalPodAutoscaler and in spec we put maxReplicas, minReplicas, scaleTargetRef, targetCPUUtilizationPercentage

### Rolling Updates
- ReplicaSet & autoscaling are important to minimize downtime and service interruptions
- Rolling updates are a way to roll out app changes in an automated and controlled fashion throughout your pods
- Work with pod templates such as deployments
- Allow for roll back if something goes wrong

To Enable:
- add liveness and readiness probes to your deployments. This ensures deployments are marked ready appropriately
- Add rolling update strategy to your YAML file

Ex of Rolling Updates:
- kubectl get pods (3 pods found hello world)
- index.js: var port = process.env.PORT || 8080; var message = process.env.MESSAGE || "Hello world!";
- Update index.js: var port = process.env.PORT || 8080; var message = process.env.MESSAGE || "Hello world v2!";
- We need to update without any downtime and allow users to access the website
- docker build -t hello-kubernetes
- docker tag hello-kubernetes upkar/hello-kubbernetes:2.0
- docker push upkar/hello-kubernetes:2.0
- kubectl get deployments
- kubectl set image deployments/hello-kubernetes hello-kubernetes=upkar/hello-kubernetes:2.0
- kubectl rollout status deployments/hello-kubernetes (sees if success)
- kubectl describe pods
- kubectl rollout undo deployments/hello-kubernetes (undo roll out)

### Config Maps and Secrets
As software developers, we know it's a good practice not to hard-code configuration variables in code. We keep them separate so that any changes in configuration do not require code changes.

index.js: var port = process.env.PORT || 8080; var message = process.env.MESSAGE || "Hello world!";
- Hard-coded values are 8080, Hello World!
- If env.PORT r env.MESSAGE found they will overwrite the hard-coded variables

ConfigMaps are used to:
- Provide configuration for deployments
- Reusable across deployments
- Created in a couple different ways:
1. Using String literals
2. Using an existing properties of "key" = "value" file
3. Providing a ConfigMap YAML descriptor file. Both the first an second ways can help us create such a YAML file
- Multiple ways to reference from Pod/Deployment (ENV variable / Mount as a Volume)

Secrets are like ConfigMaps but meant for sensitive informations

How to create ConfigMaps?
- kubectl create configmap my-config --from-literal=MESSAGE="hello from first configmap"

env:

- name: MESSAGE
- 
  valueFROM:
  
    configMapKeyRef:
  
      name: my-config
  
      key: MESSAGE

- We can list all configmaps using kubectl get configmaps
- We can get details of config map using kubectl describe configmap my-config

Another way to add MESSAGE var is:
- cat my.properties
1. MESSAGE=hello from the my.properties files
- k create cm my-config --from-file=my.properties

env:

- name: MESSAGE

  valueFROM:
  
    configMapKeyRef:
  
      name: my-config
  
      key: my.properties

  Another way:
  - kubectl get cm
  - No resources found in default namespace.
  - cat my-config.yaml
  1. apiVersion: v1
  2. data:
  3.   my.properties:MESSAGE=hello from the my.properties file
  4.   kind: ConfigMap
  5.   metadata:
  6.     name: my-config
  7.     namespace: default
  
