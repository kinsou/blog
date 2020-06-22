title: 开启Docker远程访问
author: ZkName
tags:
  - Docker
categories: []
date: 2017-07-27 10:20:00
---
###### 编辑文件 vi /etc/default/docker
```shell
# Here in Debian, this file is sourced by:
#   - /etc/init.d/docker (sysvinit)
#   - /etc/init/docker (upstart)
#   - systemd's docker.service

# Use of this file for configuring your Docker daemon is discouraged.

# The recommended alternative is "/etc/docker/daemon.json", as described in:
#   https://docs.docker.com/v1.11/engine/reference/commandline/daemon/#daemon-configuration-file

# If that does not suit your needs, try a systemd drop-in file, as described in:
#   https://docs.docker.com/v1.11/engine/admin/systemd/#custom-docker-daemon-options
# 增加

DOCKER_OPTS="-H=unix:///var/run/docker.sock -H=0.0.0.0:2375"
```