---
title: "Getting started with Kubernetes on Mac"
header:
  teaser: "/assets/images/docker-kubernetes.png"
  show_overlay_excerpt: false
---
## Objectives
* Install Docker Community Edition from Edge Channel
* Enable Kubernetes

## Installation
Docker Community Edition for Mac now comes with [Kubernetes support via the Edge channel](https://blog.docker.com/2018/01/docker-mac-kubernetes/).

You can verify if you already have Kubernetes support by checking the **Docker -> About** section and looking for the Kubernetes version to be listed.

![docker kubernetes about](/assets/images/docker-cube-about.png)

If you do not have it installed yet simply head over to the docker install page and choose the edge channel.

[https://download.docker.com/mac/edge/Docker.dmg](https://download.docker.com/mac/edge/Docker.dmg)

Once you have Kubernetes installed you will need to enable it in your **Docker -> Preferences**
![docker kubernetes enable](/assets/images/kubernetes-enable.png)

Verify kubectl is setup and pointing to the correct context for Docker.
```shell
$ kubectl config get-contexts
CURRENT   NAME                 CLUSTER                      AUTHINFO             NAMESPACE
*         docker-for-desktop   docker-for-desktop-cluster   docker-for-desktop
```

Congratulations you now have Docker dev environment that supports building both docker-compose and Swarm-based apps, as well as apps destined for deployment on Kubernetes. All container tasks – build, run and push – will run on the same Docker instance with a shared set of images, volumes and containers.
