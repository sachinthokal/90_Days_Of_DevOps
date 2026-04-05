## Task 1: Resource Requests and Limits

```yml
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
  - name: alpine
    image: alpine
    command: ["sleep", "3600"]
    resources:
      requests:
        cpu: "100m"
        memory: "128Mi"
      limits:
        cpu: "250m"
        memory: "256Mi"

```

## Task 2: OOMKilled — Exceeding Memory Limits

```yml
apiVersion: v1
kind: Pod
metadata:
  name: oom-demo
spec:
  containers:
  - name: stress
    image: polinux/stress
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "200M", "--vm-hang", "1"]
    resources:
      limits:
        memory: "100Mi"
```

## Task 3: Pending Pod — Requesting Too Much

```yml
apiVersion: v1
kind: Pod
metadata:
  name: greedy-pod
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      requests:
        cpu: "100"
        memory: "128Gi"
```

## Task 4: Liveness Probe

```yml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
      failureThreshold: 3
```

## Task 5: Readiness Probe

```yml
apiVersion: v1
kind: Pod
metadata:
  name: readiness-http
  labels:
    app: ready-test
spec:
  containers:
  - name: nginx
    image: nginx
    readinessProbe:
      httpGet:
        path: /
        port: 80
      periodSeconds: 5
```

## Task 6: Startup Probe

```yml
apiVersion: v1
kind: Pod
metadata:
  name: startup-demo
spec:
  containers:
  - name: slow-app
    image: busybox
    args:
    - /bin/sh
    - -c
    - sleep 20 && touch /tmp/started && sleep 600
    startupProbe:
      exec:
        command: ["cat", "/tmp/started"]
      periodSeconds: 5
      failureThreshold: 12
    livenessProbe:
      exec:
        command: ["cat", "/tmp/started"]
      periodSeconds: 5
```

## Task 7: Clean Up

```
kubectl delete pod resource-demo oom-demo greedy-pod liveness-exec readiness-http startup-demo
kubectl delete svc readiness-svc
```
---