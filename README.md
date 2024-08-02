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

 -Using ReplicaSets
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
