---
title: "Helm"
description: ""
lead: ""
date: 2022-01-14T00:20:38Z
lastmod: 2022-01-14T00:20:38Z
draft: false
images: []
menu: 
  docs:
    parent: "getting-started"
weight: 4
toc: true
---

## What is Helm?

[Helm](https://helm.sh/) is a tool for deploying reusable components to Kubernetes clusters.
The [introduction to Helm](https://helm.sh/docs/intro/) is a good starting point for working with Helm

## Installation

## Helm Repo Structure

Typical helm repo will have below structure -

```bash
.
|____environments # Configuration for the environments
| |____shared
| | |____shared-values.yaml # Shared values to be used across all environments
| |____stage # configuration for Stage
| | |____stage-values.yaml
| |____alpha
| | |____alpha-values.yaml
|____Chart.yaml # Defines Chart metadata and versions. Update versions using semantic versioning
|____.helmignore # Helm file for if the chart is packaged into a zip not always required
|____README.md # Containing information about how to apply the chart and what the configurable values do
|____templates # A folder containing the kuberentes mainfests that will be configured with passed values 
# Structure can be unique to chart. Changes here impact the logic of the chart 
| |____deployment.yaml # example file
| |____'_helpers.tpl' # without quotes. Contains variable transformations for convenience in the other templates
| |____NOTES.txt # Defines output to console as chart is deployed
|____values.yaml # Defines default values that came from the original chart generally you should not change these as it can have a wide impact
```

## Useful Commands

List the helm deployments -

```bash
helm list
```

Upgrade helm chart -

```bash
helm upgrade -i [release-name] [path-to-chart.yaml/.] -n [deploy-namespace] --values=environments/shared/shared-values.yaml --values=environments/alpha/[env-name]-values.yaml
```