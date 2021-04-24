---
title: "Architecture"
description: "Haaukins Platform"
lead: ""
date: 2021-04-24T01:29:01+02:00
lastmod: 2021-04-24T01:29:01+02:00
draft: false
images: []
menu: 
  docs:
    parent: "haaukins"
weight: 100
toc: true
---

> Note that following architecture is valid after version 1.8.1 on Haaukins platform. Earlier architecture version can be seen here : [Old Architecture until version 1.8.1](https://github.com/aau-network-security/haaukins/wiki/Architecture-of-Haaukins-(until-version-1.8.1))


Haaukins is evolved in time and it started to have some microservices which are mainly; 

- [haaukins-store](https://github.com/aau-network-security/haaukins-store) - This is a microservice where all event and team data is stored. The communication with Haaukins is made through gRPC calls which are available on haaukins-store. You may want to check this out from its own repository.


- [haaukins-exercises](https://github.com/aau-network-security/haaukins-exercise) - This is another microservice which contains all exercises information. The communication with Haaukins is made through gRPC calls which are available on haaukins-exercises. You may want to check this out from its own repository. 


- [gwireguard](https://github.com/aau-network-security/gwireguard) - This is another microservice which enables VPN functionality with gRPC calls. You may want to check this out from its own repository. 

## Overall Architecture of Haaukins


<img src="https://camo.githubusercontent.com/9b882b10ce1c9bfba139e2ea4b15cf7570e7bdb8dedaa2bbea96a2aef0922202/68747470733a2f2f616d3370617030303466696c65732e73746f726167652e6c6976652e636f6d2f79346d56544f3361357564505f777075526d4746416256635a4d78796f4d56726e4a42314454725564493863384a43657965587058397069747338542d7233686a366835504b477832367461716d4f676351754b764f586a4970454b6f5f777a6b714b6d65614c44666e7668734339645758634858533662756e416557444972543972366b50434d7034706e796d43472d757337584646533439416f37587371715563515a4238674e59575a5f4368544f347657586d5845416a4277645630316452393f77696474683d31303234266865696768743d3730302663726f706d6f64653d6e6f6e65" style="max-height: 700px; max-width: 700px;" />

