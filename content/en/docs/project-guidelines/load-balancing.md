---
title: "Load Balancing"
description: ""
lead: ""
date: 2022-01-14T21:55:22Z
lastmod: 2022-01-14T21:55:22Z
draft: false
images: []
menu: 
  docs:
    parent: "project-guidelines"
weight: 4
toc: true
---

## EKS

Mis-configured Load balancers can expose the service to the wider internet.

For full information on configuring a load balancer read the offcial k8s documentation.

### Prevent Exposure to 0.0.0.0/0

AWS load balancers are automatically exposed to the wider internet. To prevent this configure the load balancer with the following annotation providing your private subnet range:

```yaml
service.beta.kubernetes.io/load-balancer-source-ranges: 10.0.0.0/16
```

Also, if you have any explicit annotation to 0.0.0.0/0 please remove it.

[Further documentation can be found in the official docs](
https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.2/guide/service/annotations/#access-control)
