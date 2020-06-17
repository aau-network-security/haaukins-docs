---
layout: default
title: Configuration
parent: Haaukins
nav_order: 1
---


- [Configuration](#configuration)
  - [Files and directory structure](#files-and-directory-structure)
    - [config.yml](#configyml)
    - [exercises.yml](#exercisesyml)
  - [frontends.yml](#frontendsyml)
  - [IP Tables Configuration](#ip-tables-configuration)

# Configuration

This page describes the process of configuring a host for running the Haaukins daemon, `hknd`.
The daemon has only been tested on a Linux host with `systemd`, but binaries for other operating systems can be build as well.

For the remainder of the Wiki, we assume a user `hknd` user exists with home directory `/home/hknd`.

## Files and directory structure

The following is the default directory structure:
```
.
|-- config.yml
|-- events
|   |-- test-10-04-19
|   |   |-- 005850db.log
|   |-- test-10-04-19.yml
|-- exercises.yml
|-- frontends.yml
|-- hknd
`-- users.yml
```
The `hknd` file is the binary, and by default is uses `config.yml` in the working directory as its primary configuration file.
The following `YAML` files must be created manually and serve as configuration files for `hknd`:

| Configuration file | Purpose                                                   |
|--------------------|-----------------------------------------------------------|
| `config.yml`       | The main configuration file                               |
| `exercises.yml`    | The specification of the exercises                        |
| `frontends.yml`    | The specification of the existing frontends               |

The `users.yml` acts as a database that stores the information of CLI users.

The `event` directory serves as a database for events, such as the registered teams, the progress of teams and the monitored mouse clicks and key strokes.

### config.yml

Example

```yaml
host:
    http: <wildcard-domain> # will be used for event creation 
    grpc: <server-endpoint> # grpc endpoint
port:
    insecure: <insecure-port>
    secure: <secure-port>

tls:
  enabled: true
  certfile: "<path-cert-file>"
  certkey: "<path-cert-key>"
  cafile: "<path-cert-ca>"

files:
  ova-directory: "<frontends.yml-file-location>"
  users-file: "<users.yml-file-location>"
  exercises-file: "<exercises.yml-file-location>"
  frontends-file: "<frontends.yml-file-location>"

db-config:
  grpc: "<database-endpint>"
  db-auth-key: <database-auth-key>
  db-sign-key: <database-sign-key>
  tls:
    enabled: true
    certfile: "<database-endpoint-cert-file-location>"
    certkey: "<database-endpoint-cert-key-location>"
    cafile: "<database-endpoint-cert-ca-location>"


sign-key: <sign-key>
docker-repositories:
- username: <private-registry-user-name>
  password: <private-registry-password>
  serveraddress: <private-registry-endpoint>
```
The daemon can listen on two different host names for the reverse proxy and the gRPC traffic.
In case a HTTPS connection is preferred, the TLS configuration must be enabled, and both the secure (HTTP) and insecure (HTTPS) port must be configured.

If TLS is enabled, the `acme` field must be filled in, which ensures that `hknd` manages the TLS certificates.

**- Note -** as of now, only Cloudflare is supported as the ACME DNS provider.

The `docker-repositories` and `ova-directory` specify from which Docker repository and path on the filesystem `hknd` retrieves the images for the virtual instances.

For all (latest) configuration options, take a look at the `Config struct` in [Golang source code](https://github.com/aau-network-security/haaukins/blob/master/daemon/daemon.go#L82).

### exercises.yml

Example

```yaml
exercises:
  - name: Cross-site Request Forgery
    tags:
    - csrf
    docker:
    - image: <image name>
      dns:
      - name: formalbank.com
        type: A
      memoryMB: 80
      flag:
      - tag: csrf-1
        name: Cross-site Request Forgery
        env: APP_FLAG
        points: 12
```
This file contains a list of all exercises that can be run on Haaukins.

For all (latest) configuration options, take a look at the `Exercise struct` in the [Golang source code](https://github.com/aau-network-security/haaukins/blob/master/store/exercise.go#L41).

## frontends.yml
Example

```yaml
frontends:
- image: kali
  memoryMB: 4096
  cpu: 2
```

Contains a list of all frontends that Haaukins.
The value of `image` can be used as a tag when creating a new event from the CLI.
The daemon searches for the path `<ova-directory>/<image name>.ova`, where `ova-directory` is retrieved from the `config.yml`, and the `image name` is provided by the CLI user.



## IP Tables Configuration

In case `hknd` does not listen on the default HTTP(s) ports (i.e. 80 and 443), you can specify forwarding rules in `iptables` as follows for HTTP
```bash 
sudo iptables -t nat -A PREROUTING -i <network interface> -p tcp -m tcp --dport 80 -j DNAT --to <ip address>:<port>
```
and HTTPS
```bash 
sudo iptables -t nat -A PREROUTING -i <network interface> -p tcp -m tcp --dport 443 -j DNAT --to <ip address>:<port>
```