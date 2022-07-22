---
title: "EMR Unknown Host Exception"
description: ""
lead: ""
date: 2022-07-22T12:34:02+01:00
lastmod: 2022-07-22T12:34:02+01:00
draft: false
images: []
menu: 
  docs:
    parent: "troubleshooting"
weight: 2
toc: true
---

Let's say your EMR job is trying to access an RDS instance, you may get ***Caused by: java.net.UnknownHostException:***.

This is because you are running your job in the wrong VPC.

Ensure that you configure your EMR job to be run in the same VPC as your resources which you are trying to access.
