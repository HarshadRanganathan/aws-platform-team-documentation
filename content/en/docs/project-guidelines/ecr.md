---
title: "ECR"
description: ""
lead: ""
date: 2022-01-14T21:54:30Z
lastmod: 2022-01-14T21:54:30Z
draft: false
images: []
menu: 
  docs:
    parent: "project-guidelines"
weight: 2
toc: true
---

## Namespaces

Namespaces are a way to group similar repositories together.

e.g. team-a/web-app, team-b/web-app, project-a/web-app

Use:

Helps to scope IAM policies so that pods running in a cluster can only pull images from a particular name-spaced repositories.

### Guidelines

ECR repositories should have namespaces for logical grouping.

## Immutability

You can configure a repository to be immutable to prevent image tags from being overwritten.

This can thwart an attacker from overwriting an image with a malicious version without changing the image's tags.

Additionally, it gives you a way to easily and uniquely identify an image.

### Guidelines

Repositories should be configured as immutable

## Lifecycle Policy

It is recommended to apply below lifecycle policy to your ECR repository so that old images are cleaned up automatically.

Untagged images --> Delete after 7 days

Tagged images --> Maintain up to 10 recent images

```json
{
    "rules": [
        {
            "rulePriority": 1,
            "description": "Rule 1",
            "selection": {
                "tagStatus": "untagged",
                "countType": "sinceImagePushed",
                "countUnit": "days",
                "countNumber": 7
            },
            "action": {
                "type": "expire"
            }
        },
        {
            "rulePriority": 2,
            "description": "Rule 2",
            "selection": {
                "tagStatus": "any",
                "countType": "imageCountMoreThan",
                "countNumber": 10
            },
            "action": {
                "type": "expire"
            }
        }
    ]
}
```
