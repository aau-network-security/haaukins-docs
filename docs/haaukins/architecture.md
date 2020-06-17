---
layout: default
title:  Architecture
parent: Haaukins
nav_order: 3
---

- [Overview](#overview)
- [Components](#components)
  - [Virtual](#virtual)
    - [Docker](#docker)
    - [Virtual Machine (VirtualBox)](#virtual-machine-virtualbox)
  - [Store](#store)
  - [Relationship](#relationship)

# Overview

Haaukins is changing its internal components in time which brings some changes in architecture side of Haaukins project. Haaukins project started to expand its components and features by splitting some functions/features. (Trying to adapt [microservice architecture](https://microservices.io/patterns/microservices.html))

Following information is valid for versions which are newer than [1.8.1](https://github.com/aau-network-security/haaukins/releases/tag/1.8.1), currently there is no release yet for new features and updates, but will soon. Note that, there could be some parts which stayed exatcly same with version older than version [1.8.1](https://github.com/aau-network-security/haaukins/releases/tag/1.8.1). 

# Components 

Haaukins has several compoenents which are crucial for Haaukins main duty, namely  virtual, store, amigo and guacamole. 

## Virtual 

Virtual is package inside Haaukins repository which is responsible for managing Docker containers and virtual machines, it has an abstraction which eliminates complexity of using Docker and VM features. Docker is used for hosting CTF (Capture The Flag) challenges, suitable challenges could be packaged into Docker image to be run in isolated environment. Virtual machines are used for creating a challenge (possible) and providing a Linux environment which is specialized version of Kali,Parrot or any customized VM which are intended to use. The provided Linux environment should contain all related tools to solve provided challenge. 

Haaukins is creating virtual network using docker network to attach VM and containers into same network, this way client who is connected to virtualized environment is able to see and solve challenges which are on same network. It can be imaged like a situation where you connected to network which has some more clients connected to same network, in this case you will be able to see and perform cyber operation to them using your own customized tools. Haaukins is providing similar scenario for you, you have some clients which are connected to same network with you and you need to perform some cyber operation in order to receive flag in totally virtualized environment. 

Virtualized environment (an event) could be summarized with following figure below. 

![Event Representation](../../../assets/images/haaukins/event-representation.png)

### Docker  

Docker is primarily used to create closed network with specified challenges, each challenge has its own docker container, in this sense no one can involve others network even they share same server. As illustrated given diagram above, blue dots represents docker containers and they have connected to same network. 

Each component of the event lives in a docker container, which provides better stability and management, spinning up containers is cheap compared to other methods, in addition docker ensures environment isolation.

In Haaukins, docker containers should share their unique network in order to prevent any abuse over other teams’ labs. To give an example, if an event is created and a team is signed up for the event, then the team is assigned to group of docker containers which are sharing same network with Kali Linux. Since they are sharing same network, the exercises on the platform can be solved on Kali over browser connection. Corresponding illustration summarizes how docker networking structured for four teams for an event.



![Lab Representation](../../../assets/images/haaukins/lab_representation.jpg)



### Virtual Machine (VirtualBox)

Virtualbox is used to manage virtual machines which are one of main component of Haaukins platform, we have created preconfigured ova file of Kali operating system, which contains all related tools to solve challenges that are existing on Haaukins platform over browser by connecting to Kali machine. In addition to docker environment described under docker subtitle, VMs automatically connect to GUAC container to give access the user to Kali machine over browser by creating RDP connection.

In given figure above __red dots__ are representing instance which has connection to [Apache Guacamole](https://guacamole.apache.org/) server which also runs in Docker environment.



## Store

Store is responsible for mananing information about events and teams, all related information could be found in [Store](../store/store.md) section. Store is also an gRPC endpoint with Postgres database connection. 



## Relationship 

Relationship diagram

In this section, relationship between different components within Haaukins platform will be illustrated and explained.

- An event can have non or multiple teams but should have at least one exercise within it.

- A team under an event will have just one virtual machine assigned to the team particularly, however the team could have multiple exercises which is directly inherited from event configuration which means that if an event created with three exercises them team will have automatically assigned to three exercises within it. Each team has its own isolated environment within Haaukins platform.

Illustration of relationship between, event, team and exercises shown below; 


![Relationship Representation](../../../assets/images/haaukins/relationship.jpg)