---
title: "Terraform"
description: ""
lead: ""
date: 2022-01-14T09:09:44Z
lastmod: 2022-01-14T09:09:44Z
draft: false
images: []
menu: 
  docs:
    parent: "getting-started"
weight: 3
toc: true
---

Terraform is used to allow users to easily and repeatably create resources. 

Creation of resources should not be done manually as this leaves a risk that they will not be repeatable should there be a failure or accidental deletion

## Tags

We require below tags to be set for resources as it'll help with easier tracing and cost tracking.

|Tag Key |Tag Value | Purpose |
|-- |-- |-- |
|Name | |Useful name to identify individual resources |
|Application ID | |Identify resources that are related to a specific application |
|Namespace/Application Role | |Resource group/Describe the function of a particular resource (such as web server, message broker, database) |
|Stage |alpha/stage/prod |Distinguish between development, test, and production resources |
|ManagedBy |terraform |Indicates the process that manages the resource |
|TF Repo |https://github.com/ |TF Repository which was used to create the resource  |
|Team |Infra Platform |Team which created the resource  |
|Owner |Infra Platform |Identify who is responsible for the resource |
|Owner DL |team@example.com |DL for issues/notifications related to the resource |
|Cost Center | |Identify the cost center or business unit associated with a resource, typically for cost allocation and tracking |
|Confidentiality |Sensitive |An identifier for the specific data confidentiality level a resource supports |