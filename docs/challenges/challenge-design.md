---
layout: default
title: Designing a challenge
parent: Challenges
nav_order: 5
---


# Designing a challange

Generally, challenges can consist of any set of docker images and VirtualBox OVA's. However, these images are constrained by the following

- The will reside on the same `/24` subnet, that in unknown to the images prior to boot.`
- It images are dependent on each other, then service discovery is conducted through DNS.
- They are unable to obtain gain internet access.
- Make sure DNS records used for service discovery is fairly unique, to avoid colliding records with other challenges.
- Docker images that are supposed to contain flags should ideally be able to receive a dynamic flag through the `APP_FLAG` environment variable (or another environment variable specified in the challenge config).

### Example of challenge configuration

```yaml
- name: Cross-Site Scripting                     # display name of challange
    tags:
    - xss                                        # list of tags that the challenge can be referenced by
    docker:                                      # set of docker images
    - image: registry.sec-aau.dk/aau/xss-client  # name of first image
      memoryMB: 512                              # required memory for container
      env:                                       # environment variables for docker container
      - env: APP_TARGET_URL
        value: https://dogshare.com
      - env: APP_USERNAME
        value: Kristy
      - env: APP_PASSWORD
        value: z!etAszv@.Izf{#ui}|Qzeffyc#!(&)zmFnmzmFTBZ,,e
    - image: registry.sec-aau.dk/aau/xss-server  # second image
      memoryMB: 85
      dns:                                       # dns records that should point to the assigned IP of the running container
      - name: dogshare.com
        type: A
      flag:                                      # flags that are contained in the container
      - tag: xss-1                               # tag of the given flag
        name: Cross-site scripting               # display name for flag
        env: APP_FLAG                            # which environment variable to send the dynamic flag by (if the flag should be static, specify `static`
        points: 15                               # points for obtaining the given flag
```
