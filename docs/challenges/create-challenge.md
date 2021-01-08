---
layout: default
title: Creating a challenge
parent: Challenges
nav_order: 0
---


# Creating a Challenge
A challenge is created as a subfolder in its category folder. A sample challenge folder is `sample/piece_of_pie/` with the contents below:
```
example/challenge_1/
|-- README.md
|-- Dockerfile
|-- .gitlab-ci.yml
|-- tests
    `-- test_exploit.py
|-- sol/
|   `-- exploit.py
|-- config (or src) /
     |-- auto.conf
     |-- init.sh
```
As above, the challenge folder must have:
* The challenge folder should contain following information and main `README.md` file. You can follow [Challenge Repository Structure ](../challenge-structure/) for an example of how the readme file should be setup for your challenge;


* a `config (or src)/` subfolder used for setting up environment for the challenge. This includes startup scripts and challenge source code (C, C#, python or whatever you chose).
* a `sol (or exploit)/` subfolder containing the solution/exploit script. Only if applicable to your challenge
* a `tests/` subfolder which will test functions which are given under `sol/`. Or manually unittesting your challenge can also be done. You just have to ensure that every bit and piece of the challenge works before pushing it to our registry.

## Technical side of creating challenge

Imagine a situation where you are using a framework in your infrastructure which is vulnerable and the exploit has been published on https://www.exploit-db.com. In order to experience what you may face by having that vulnerability,  a simulation environment could be set up by using docker containers. Steps could differ challenge to challenge however, most of the steps are same for all kind of challenges. Prerequisites of creating a challenge consists of having knowledge about docker environment and basic programming skills.



Steps for creating a challenge could be summarized as shown below:

1.  Define a challenge to create, let's consider the one which is `Webmin 1.920 - Unauthenticated Remote Code Execution (Metasploit)` (https://www.exploit-db.com/exploits/47230).
2. In order to create the given challenge, examine layers (environment ~ operating system, specific version of program and etc ) which could be needed to run vulnerable `Webmin` on docker container.
3. Once all explanation is examined through https://www.exploit-db.com, make a list of them and started to implement on docker file.

* _Linux operating system (could Ubuntu 18.04 ) since there is no specification of the version of operating system which will handle php on it_

* The vulnerability itself requires to have perl language on top of operating system therefore it will be the second step to install.

* Since the mentioned vulnerability requires webmin 1.920 version then, it should be installed it by using install instructions which are already exists on webmin official page. Just install it using source code, in order to have vulnerability in a containerized environment.

* Afterwards all configuration settings will be based on kind of challenge that you are writing, define bash script which handles all configuration things regarding to webmin, php, perl.

* In bash script, an environment variable should be declared in order to provide it to Haaukins itself, so the provided environment variable will be used to create dynamic flags. Example:

  - `$APP_FLAG` , in Haaukins side, Haaukins will generate unique UUID flag for given environment variable.

Example Dockerfile for a challenge which describes how the vulnerability of `webmin 1.920` framework can be simulated using dockerfile.

Before starting to write Dockerfile, you either need to download the package to your local and copy it into container or you can fetch that using `curl` and download it into container directly. In this example, we are assuming that you have already downloaded the freamwork (webmin 1.920)

`Dockerfile`

```
FROM ubuntu:18.04   // this is base layer for our containerized environment...
FROM perl:5.20      // adding additional software on top of base layer in order to run webmin, so this is a prerequisite
COPY webmin-1.920.tar.gz  .  // which is copying tar.gz file into container.

RUN gunzip  webmin-1.920.tar.gz && \
    tar xf wembin-1.920.tar && \
    cd webmin-1.920 && \
    ./setup.sh  /usr/local/webmin    //  setup.sh is default setup script for webmin-1.920, so it is already inside tar.gz

COPY /etc/webmin/config .           // copying configuration files into docker container
COPY /etc/webmin/miniserv.conf .    // copying configuration files into docker container

COPY run.sh .  // this is the bash script where all configuration files has been set with the flag.

RUN chmod +x run.sh  // change permission of the run.sh script

CMD ["./run.sh"]   // starting point of webmin-1.920 framework.

```
`run.sh`    

```

#!/bin/sh

cp config /etc/webmin
cp miniserv.conf /etc/webmin
echo " $APP_FLAG" >> /var/flag.txt
unset APP_FLAG                # this is crucial to unset, otherwise a user can print all environment variables and can get the flag.
echo Starting webmin
/etc/init.d/webmin start
while :; do echo 'Press <CTRL+C> to exit.'; sleep 1; done  

```

More things to keep in mind, the networking setting should not be overlap, otherwise, the challenge cannot be imported into Haaukins environment properly. Please consider following matters as well, while constructing a challenge in a containerzed environment.


Generally, challenges can consist of any set of docker images and VirtualBox OVA's. However, these images are constrained by the following

  - They will reside on the same /24 subnet, that in unknown to the images prior to boot.`
  - Make sure DNS records used for service discovery is fairly unique, to avoid colliding records with other challenges.
  - Docker images that are supposed to contain flags should ideally be able to receive a dynamic flag through the APP_FLAG  environment variable (or another environment variable specified in the challenge config).

Note that the given examples differs challenge to challenge, however the concept is same, build vulnerable enviroment in docker (containerized docker environment) and then set flag environment into a file or somewhere, lastly do not forget to unset flag from environment once setting the flag to a file process is done.

For further assistance, please contact us by creating an issue regarding to creating  a challenge, under wiki (this repository).

_(Please declare your situation as much detalied as possible, otherwise we may face a deadlock where nobody can benefit from it. )_




## Deploying a Challenge
Deploying challenges from gitlab is very easy, you can use the following template and put it into the `.gitlab-ci.yml` file;
```
docker-push-to-gitlab-registery:
  image: docker:latest
  stage: build
  services:
    - docker:dind
  before_script:
    - docker login -u "$CI_USER" -p "$CI_TOKEN" $GITLAB_REGISTERY
  script:
    - docker build --pull -t "$GITLAB_REGISTERY/haaukins/challenge_category/challengerepo" .
    - docker push "$GITLAB_REGISTERY/haaukins/challenge_category/challengerepo"
  only:
    - master
```

