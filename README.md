![](https://github.com/dounine/standalone-chrome-ssl/workflows/Publish%20Docker%20image/badge.svg) ![](https://img.shields.io/github/license/dounine/standalone-chrome-ssl)

# standalone-chrome-ssl

## Introduction
The selenium/standalone-chrome version does not support ssl blocking by default, and this version is supported.

## Useage
docker pull
```
docker pull dounine/standalone-chrome:1.0
```
docker run
```
docker run -d -p 4444:4444 --shm-size 2g dounine/standalone-chrome:1.0
```
