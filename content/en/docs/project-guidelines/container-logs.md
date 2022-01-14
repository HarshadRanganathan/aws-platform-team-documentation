---
title: "Container Logs"
description: ""
lead: ""
date: 2022-01-14T21:55:09Z
lastmod: 2022-01-14T21:55:09Z
draft: false
images: []
menu: 
  docs:
    parent: "project-guidelines"
weight: 3
toc: true
---

In the process of containerization, we should keep in mind that, the container is going to run anywhere in cloud environment.

In general, teams will use Kubernetes or any other services to run the containers.

These services have been enabled with built-in log forwarding of STDOUT/STDERR from containers to external services such as Cloudwatch, Splunk, ES etc.

So, it's recommended to just write your logs to STDOUT/STDERR.

For example, you could have your `log4j2.xml` configured as follows:

```xml
<Console name="LogToConsole" target="SYSTEM_OUT">
  <PatternLayout>
    <Pattern>{ "date_time":"%date", "thread":"[%thread]", "log_level":"%-5level", "class_name":"%logger{0}", "log_message":"%msg" }%n</Pattern>
  </PatternLayout>
</Console>
```

If you are running your containers in EKS, logs written to STDOUT/STDERR will automatically be rotated and cleared at regular intervals/based on size.

{{<alert icon="⚠️" text="Do not write logs to the local file system!!" />}}

e.g.

```xml
<File name="LogToFile" fileName="logs/log.txt">
  <PatternLayout>
    <pattern>{ "date_time":"%date","log_message":"%msg" }%n</pattern>
  </PatternLayout>
</File>
```

Above will result in `DiskPressure` and will crash your nodes as the log size grows and you don't have any custom mechanism to rotate and clear the logs.