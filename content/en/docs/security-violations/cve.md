---
title: "CVE"
description: ""
lead: ""
date: 2022-07-22T12:55:52+01:00
lastmod: 2022-07-22T12:55:52+01:00
draft: false
images: []
menu: 
  docs:
    parent: "security-violations"
weight: 3
toc: true
---

If any security vulnerabilities are being reported for any EC2 instances, similar to below,

```
CVE-2020-27619 - python, python-devel and 4 more
CVE-2021-33574 - glibc-minimal-langpack, glibc-devel and 6 more
CVE-2022-1154 - vim-minimal, vim-common and 2 more
CVE-2022-22965 - org.springframework:spring-webmvc
CVE-2021-22945 - libcurl, curl
```

then we'd need to update the libraries within the EC2 instance. To do that, SSH into the EC2 instance, and run below command:

```bash
sudo yum update -y
```

which updates all the libraries to the latest version and will resolve all of the security vulnerabilities.

In some cases, you may also see below Kernel vulnerability.

```
CVE-2022-29581 - kernel
```

The above update command also updates the Kernel, but a reboot of the EC2 instance is required to apply the Kernel update.
