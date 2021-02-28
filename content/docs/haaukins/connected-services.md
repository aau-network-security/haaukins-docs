---
title: "Connected Services"
description: "Services used by Haaukins Platform"
lead: ""
date: 2020-10-13T15:21:01+02:00
lastmod: 2021-02-28T21:16:01+02:00
draft: false
images: []
menu: 
  docs:
    parent: "haaukins"
weight: 100
toc: true
---

Haaukins is using few services to operate its ordinary workload. There are three different services which Haaukins is using namely, haaukins-store, haaukins-exercises, haaukins-webclient. 

## Haaukins Webclient 

This is **NOT** a mandatory service for Haaukins to work. It is implementation of CLI on web, it is using Envoy Proxy with gRPC. Detailed information regarding to it and source code can be found following link here: [haaukins-webclient](https://github.com/aau-network-security/haaukins-webclient)

## Haaukins Store 

This is a service which is using PostreSQL with gRPC. Detailed information and source code can be found following link: [haaukins-store](https://github.com/aau-network-security/haaukins-store). Without haaukins-store, Haaukins can **NOT** work from version [2.0.0](https://github.com/aau-network-security/haaukins/releases/tag/2.0.0)


## Haaukins Exercises 

This is a service which is using MongoDB with gRPC. Detailed information and source code can be found following link: [haaukins-exercises](https://github.com/aau-network-security/haaukins-exercises). Without haaukins-exercise, Haaukins can **NOT** work from version [2.4.0](https://github.com/aau-network-security/haaukins/releases/tag/2.4.0)

