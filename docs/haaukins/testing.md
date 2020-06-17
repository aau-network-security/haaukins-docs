---
layout: default
title:  Testing
parent: Haaukins
nav_order: 4
---


# Testing 

Please stick to using Go's [testing package](https://golang.org/pkg/testing/) conventions.

Before using any third party libraries for testing, please make sure they are strictly necessary.

For integration tests, use the practice described [here](https://stackoverflow.com/a/41407042).

TLDR: Use `go test -short ./...` (unit tests only) mostly. Use `go test ./...` for full testing suite (including integration tests).