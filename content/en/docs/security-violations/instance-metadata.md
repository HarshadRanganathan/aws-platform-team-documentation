---
title: "Instance Metadata"
description: ""
lead: ""
date: 2022-07-22T12:53:06+01:00
lastmod: 2022-07-22T12:53:06+01:00
draft: false
images: []
menu: 
  docs:
    parent: "security-violations"
weight: 1
toc: true
---

To block Instance Metadata v1 from being by an EC2 instance post creation, run below command:

```bash
aws ec2 modify-instance-metadata-options --instance-id ${INSTANCE_ID} --http-tokens required --http-endpoint enabled
```
