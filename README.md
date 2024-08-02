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

