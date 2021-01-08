---
layout: default
title: Challenge Repository Structure
parent: Challenges
nav_order: 1
---

# Repository title
Describe what the challenge is about, any relevant CVE's, which tools should be used for the challenge, etc.

# Domain name
If the challenge does not have NMAP as a part of the challenge, the general rule of thumb is, that it should have a domain name. This is to easily distinguish challenges from each other when there is a lot of them running on the platform.
The domain name should then also be included in the challenge description(s) for the user to easily access the challenge.

`domain-name-here.com`

# Descriptions
The challenge descriptions are what is actually going to be displayed on the platform, and it should have a challenge name and a description for each flag the challenge haves;

1. **Name of challenge_1**
* Proposed difficulty: "Whatever difficulty you beleive that the challenge is"
* This should be the description of the challenge for the first flag in multi flag challenges. This is also here the user should be instructed to browse a specific domain and protocol in order to find the challenge.

2. **Name of challenge_2**
* Proposed difficulty: "Whatever difficulty you beleive that the challenge is"
* Description here

3. **Name of challenge_n**
* Proposed difficulty: ......
* Description here

# Prerequisites and Outcome

**Prerequisites**

* Some prerequisite
* Some prerequisite
* Some prerequisite

**Outcome**

* Some Outcome
* Some Outcome
* Some Outcome

# How to run on local machine
```
$ git clone https://gitlab.com/haaukins/challenge_category/challengerepo.git
$ cd challengerepo
$ docker build -t cd challengerepo .
$ docker run -d -p port:port -e APP_FLAG="FLAG1" -e APP_FLAG2="FLAG2" -e APP_FLAGn="FLAGn" challengerepo
```

# Solutions

## Flag1
* Write the solution in bulletpoints for each step the user should take.

## Flag2
* Write the solution in bulletpoints for each step the user should take.
