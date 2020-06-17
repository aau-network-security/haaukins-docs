---
layout: default
title:  Specifications
parent: Webclient
nav_order: 1
---

- [Specification](#specification)
  - [How it works](#how-it-works)
  - [Docker compose specifications](#docker-compose-specifications)
  - [Envoy Proxy Configuration](#envoy-proxy-configuration)


# Specification

Haaukins web client is transformed form of CLI client in Haaukins, basically all specifications which are belong to CLI of Haaukins exists for Haaukins Web Client as well. 

## How it works 

It uses Envoy proxy to use web gRPC with existing gRPC proto file which exists on Haaukins project. Envoy proxy stands in front of the application in order to convert standart HTTP requests into gRPC. 

![Communication Diagram](/assets/images/webclient/webclient-arch.png)

The communication between Envoy Proxy and Server is made with gRPC calls, Envoy is responsible to transform HTTP requests to gRPC requests. Web client resides on Docker image with all dependencies and it is used as service by docker compose. 



## Docker compose specifications

- `nginx` is used for managing domain and incoming requests which are NOT gRPC. 
  
- `envoy ` service is used for gRPC calls. 
  
- `webclient` contains VueJS components which makes frontend residing and consistent. 



```yaml 

version: '3.4'
services:
  proxy:
    build:
      context: ./envoy
      dockerfile: Dockerfile
    ports:
      - '8000:8000'
    volumes:
      - ${CERTIFICATES_PATH}:/etc/certs
    networks:
      - haaukins-webclient
    env_file:
      - .env

  webclient:
    build:
      context: ./client
      dockerfile: Dockerfile
      target: build-stage
    networks:
      - haaukins-webclient

  nginx:
    build:
      context: ./client
      dockerfile: Dockerfile
      target: production-stage
    ports:
      - '8003:8003'
    volumes:
      - ${CERTIFICATES_PATH}:/etc/certs
    networks:
      - haaukins-webclient
    env_file:
      - .env
networks:
  haaukins-webclient:

```

## Envoy Proxy Configuration 

Envoy is currently has following configuration for WebClient. However, it may change in time when required, it is actually also possible to use only envoy proxy for the web client, nginx is could be removed since envoy can handle both gRPC and HTTP requests. 

HTTP/1 requests through the Envoy sidecar process which are upgraded into HTTP/2 gRPC requests.

The role of Envoy proxy can be illustrated better with following figure: 

![Envoy Proxy Role](/assets/images/webclient/envoy-example.png)



```yaml 

admin:
  access_log_path: /tmp/admin_access.log
  address:
    socket_address: { address: 0.0.0.0, port_value: 9901 }
static_resources:
  listeners:
    - name: listener_0
      address:
        socket_address: { address: 0.0.0.0, port_value: 8000 }
      filter_chains:
        - filters:
          - name: envoy.http_connection_manager
            config:
              codec_type: auto
              stat_prefix: ingress_http
              route_config:
                name: local_route
                virtual_hosts:
                  - name: local_service
                    domains: ["*"]
                    routes:
                      - match: { prefix: "/" }
                        route:
                          cluster: greeter_service
                          max_grpc_timeout: 0s
                    cors:
                      allow_origin_string_match:
                      - safe_regex:
                          google_re2: {}
                          regex: \*
                      allow_methods: GET, PUT, DELETE, POST, OPTIONS
                      allow_headers: keep-alive,user-agent,cache-control,content-type,content-transfer-encoding,custom-header-1,x-accept-content-transfer-encoding,x-accept-response-streaming,x-user-agent,x-grpc-web,grpc-timeout,x-custom-header,token
                      max_age: "1728000"
                      expose_headers: token,custom-header-1,grpc-status,grpc-message
              http_filters:
                - name: envoy.grpc_web
                - name: envoy.cors
                - name: envoy.router
                  config: {}
          tls_context:
            common_tls_context:
              alpn_protocols: "h2"
              tls_certificates:
                - certificate_chain:
                    filename: "/etc/certs/fullchain.pem"
                  private_key:
                    filename: "/etc/certs/privkey.pem"
  clusters:
    - name: greeter_service
      connect_timeout: 0.25s
      type: strict_dns
      http2_protocol_options: {}
      lb_policy: round_robin
      hosts: [{ socket_address: { address: 172.17.0.1, port_value: 5454 }}]
      tls_context:
        common_tls_context:
          tls_certificates: 
            certificate_chain: {"filename": "/etc/certs/fullchain.pem"}
            private_key: {"filename": "/etc/certs/privkey.pem"}

```

