---
title: "Kubernetes Probes"
description: ""
lead: ""
date: 2022-01-14T21:55:46Z
lastmod: 2022-01-14T21:55:46Z
draft: false
images: []
menu: 
  docs:
    parent: "project-guidelines"
weight: 6
toc: true
---

We recommend that you set below probes for your deployment.

## StartUp Probe

<div class="alert alert-light" role="alert">
  <h4 class="alert-heading">Note</h4>
  <p>
  If the startup probe never succeeds, the container is killed after 300s and subject to the pod's restartPolicy.

  Set up startup probe with a `failureThreshold * periodSeconds` long enough to cover the worse case startup time
  </p>
</div>

The kubelet uses startup probes to know when a container application has started.

If such a probe is configured, it disables liveness and readiness checks until it succeeds, making sure those probes don't interfere with the application startup.

This can be used to adopt liveness checks on slow starting containers, avoiding them getting killed by the kubelet before they are up and running.

```yaml
spec:
  template:
    spec:
      containers:
        - name: {{ .Chart.Name }}
          startupProbe:
            httpGet:
              path: /health
              port: http
              scheme: HTTP
            timeoutSeconds: 10    # number of seconds before marking the probe as timing out (failing the health check)
            periodSeconds: 10     # how often to check the probe
            successThreshold: 1   # minimum number of consecutive successful checks
            failureThreshold: 30  # number of retries before marking the probe as failed
```

In above configuration, the probe checks /health endpoint every 10 seconds until 5 mins `(periodSeconds * failureThreshold = 300s)`.

Within that period if the health check endpoint returns success, then it would turn on liveness and readiness probes. Otherwise, it would fail.

## Readiness Probe

<div class="alert alert-light" role="alert">
  <h4 class="alert-heading">Note</h4>
  <p>
  Kubernetes makes sure the readiness probe passes before allowing a service to send traffic to the pod.

  If a readiness probe starts to fail, Kubernetes stops sending traffic to the pod until it passes.
  </p>
</div>

Readiness probes are designed to let Kubernetes know when your app is ready to serve traffic.

```yaml
spec:
  template:
    spec:
      containers:
        - name: {{ .Chart.Name }}
          readinessProbe:
            httpGet:
              path: /health
              port: http
              scheme: HTTP
            timeoutSeconds: 10
            periodSeconds: 10
            successThreshold: 1
            failureThreshold: 3
```

## Liveness Probe

<div class="alert alert-light" role="alert">
  <h4 class="alert-heading">Note</h4>
  <p>
  We recommend you use a startupProbe along with a liveness probe.

  If your liveness probe fails, it will restart your container.

  Incorrect configuration (e.g. App takes more time to startup than the configured delays) will result in a constant restart loop.
  </p>
</div>

```yaml
spec:
  template:
    spec:
      containers:
        - name: {{ .Chart.Name }}
          livenessProbe:
            httpGet:
              path: /health
              port: http
              scheme: HTTP
            timeoutSeconds: 10
            periodSeconds: 10
            successThreshold: 1
            failureThreshold: 3
```