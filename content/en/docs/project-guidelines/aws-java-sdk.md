---
title: "AWS Java SDK"
description: ""
lead: ""
date: 2022-01-14T21:53:33Z
lastmod: 2022-01-14T21:53:33Z
draft: false
images: []
menu: 
  docs:
    parent: "project-guidelines"
weight: 1
toc: true
---

## Minimum SDK

It is recommended to use a minimum SDK version of `1.11.704` or above in your projects.

<div class="alert alert-warning" role="alert">
  <h4 class="alert-heading">Error</h4>
  <p>
  Using an SDK below the minimum recommended version will cause your app to fail with Unable to locate credentials error.

  This is because we have disabled IMDS v1 (Instance metadata service used by your SDK to get credentials) for security reasons.

  Latest SDK versions use IMDS v2 for getting the credentials.
  </p>
</div>

## FAQs

I have updated my application to use the latest SDK version but it still fails with `Unable to locate credentials` error.

Your application might still be using an older SDK version. Try below steps to fix the problem.

- Run `mvn dependency:tree` to view the hierarchy of project dependencies and add exclusions in your POM to remove older SDK dependencies.

- Override the dependency via maven dependencyManagement section.

e.g.

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
          <groupId>com.amazonaws</groupId>
          <artifactId>aws-java-sdk-core</artifactId>
          <version>1.11.1000</version>
          <scope>compile</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```
