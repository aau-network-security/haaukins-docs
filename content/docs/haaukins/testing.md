---
title: "Testing"
description: "Haaukins Platform"
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

Please stick to using Go's [testing package](https://golang.org/pkg/testing/) conventions.

Before using any third party libraries for testing, please make sure they are strictly necessary.

For integration tests, use the practice described [here](https://stackoverflow.com/a/41407042).

TLDR: Use `go test -short ./...` (unit tests only) mostly. Use `go test ./...` for full testing suite (including integration tests).